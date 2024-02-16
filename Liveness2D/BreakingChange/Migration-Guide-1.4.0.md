# Liveness 1.4.0 - Guia de migração

#### Guia de migração para a versão 1.4.0 da SDK Liveness Android.

1. Com a adição do enum `FaceCaptchaErrorCode`, agora a forma de identificação dos erros retornados pelo SDK está mais consistente. Os erros podem ser verificados como no exemplo abaixo:

```kotlin
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    super.onActivityResult(requestCode, resultCode, data)

    if (requestCode == CAPTCHA_RESULT_REQUEST) {
        when (resultCode) {
            Activity.RESULT_OK -> onResultSuccess(data)
            Activity.RESULT_CANCELED -> onResultCancelled(data)
        }
    }
}

private fun onResultCancelled(data: Intent?) {

    val errorMessage = data?.getStringExtra(FaceCaptchaActivity.PARAM_RESULT_ERROR)
    val errorCode = data?.getSerializableExtra(FaceCaptchaActivity.PARAM_RESULT_ERROR_CODE) as? FaceCaptchaErrorCode

    errorCode?.let {

        Toast.makeText(this, "Código de Erro: $it\n\nMensagem: $errorMessage", Toast.LENGTH_LONG).show()

        when (it) {
            FaceCaptchaErrorCode.INVALID_BUNDLE_PARAMS -> Log.d(TAG, "Error code: INVALID_BUNDLE_PARAMS")
            FaceCaptchaErrorCode.INVALID_APP_KEY -> Log.d(TAG, "Error code: INVALID_APP_KEY")
            FaceCaptchaErrorCode.CERTIFACE_OFF -> Log.d(TAG, "Error code: CERTIFACE_OFF")
            FaceCaptchaErrorCode.NO_FRONT_CAMERA -> Log.d(TAG, "Error code: NO_FRONT_CAMERA")
            FaceCaptchaErrorCode.NO_CAMERA_PERMISSION -> Log.d(TAG, "Error code: NO_CAMERA_PERMISSION")
            FaceCaptchaErrorCode.NO_INTERNET_CONNECTION -> Log.d(TAG, "Error code: NO_INTERNET_CONNECTION")
            FaceCaptchaErrorCode.PHONE_CALL_IN_PROGRESS -> Log.d(TAG, "Error code: PHONE_CALL_IN_PROGRESS")
            FaceCaptchaErrorCode.REQUEST_ERROR -> Log.d(TAG, "Error code: REQUEST_ERROR")
            FaceCaptchaErrorCode.CHALLENGE_INTERRUPTED -> Log.d(TAG, "Error code: CHALLENGE_INTERRUPTED")
            FaceCaptchaErrorCode.LOW_MEMORY -> Log.d(TAG, "Error code: LOW_MEMORY")
        }
    }
}
```

Os erros podem assumir os seguintes valores:

```kotlin
/**  
 * Erros que podem ser retornados pelo FaceCaptcha.
 */
enum class FaceCaptchaErrorCode {  
    // Parâmetros inválidos  
    INVALID_BUNDLE_PARAMS,  
    // App Key inválido.  
    INVALID_APP_KEY,  
    // Certiface offline.  
    CERTIFACE_OFF,  
    // Aparelho não possui câmera frontal  
    NO_FRONT_CAMERA,  
    // Não foi concedida permissão de acesso à câmera do aparelho.  
    NO_CAMERA_PERMISSION,  
    // Sem conexão à Internet.  
    NO_INTERNET_CONNECTION,  
    // Chamada telefônica em andamento. Não é possível iniciar o desafio durante uma chamada telefônica.  
    PHONE_CALL_IN_PROGRESS,  
    // Erro na requisição.  
    REQUEST_ERROR,  
    // App foi minimizado durante o uso do FaceCaptcha, isso faz com que o desafio seja encerrado.  
    CHALLENGE_INTERRUPTED,  
    // Memória do aparelho está baixa  
    LOW_MEMORY  
}
```
