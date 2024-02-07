# Liveness 9.0.0 - Guia de migração

#### Guia de migração para a versão 9.0.0 do SDK Liveness Android.

### Atualizações

- Atualizado PARAM_FONTS agora pode receber tanto um hashmap com o path da fonte quanto um hashmap contendo o resource ID.
- `PARAM_FONTS_NEW_API` removido.
- Removida validação onde era possivel implementar o `PARAM_FONTS_NEW_API` somente com api superiores a 26 agora presente no `PARAM_FONTS`.

### Exemplo de implementação

Seguindo a documentação gerada na versão [8.0.0](https://github.com/oititec/liveness-android-sdk/edit/main/Documentation/Migration-Guide-8.0.0.md), foi aprimorada a forma como são passadas as fontes agora o `PARAM_FONTS `e `PARAM_FONTS_NEW_API ` passaram a ser um só, recebendo um hash map de string com o path da fonte ou com a referencia do resource como nos exemplos abaixo:

### Passando o Resource id da fonte:
```kotlin
val fonts = hashMapOf(
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_HEADER_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_SUBTEXT_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_READY_SCREEN_HEADER_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_READY_SCREEN_SUBTEXT_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_RETRY_SCREEN_HEADER_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_RETRY_SCREEN_SUBTEXT_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.RESULT_SCREEN_CUSTOMIZATION_MESSAGE_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_BUTTON_FONT to R.font.vinasans_regular,
            Liveness3DFontsKey.FEEDBACK_CUSTOMIZATION_TEXT_FONT to R.font.vinasans_regular
        )
        
        startActivityForResult?.launch(Intent(this, Liveness3DActivity::class.java).apply {
            putExtra(Liveness3DActivity.PARAM_LIVENESS3D_USER, liveness3DUser)
            putExtra(Liveness3DActivity.PARAM_FONTS, fonts)
        })
```
## Passando o path da pasta assets:
```kotlin
val fontsFromAssets = hashMapOf(
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_HEADER_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_SUBTEXT_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_READY_SCREEN_HEADER_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_READY_SCREEN_SUBTEXT_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_RETRY_SCREEN_HEADER_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_RETRY_SCREEN_SUBTEXT_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.RESULT_SCREEN_CUSTOMIZATION_MESSAGE_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.GUIDANCE_CUSTOMIZATION_BUTTON_FONT to "fonts/vinasans_regular.ttf",
            Liveness3DFontsKey.FEEDBACK_CUSTOMIZATION_TEXT_FONT to "fonts/vinasans_regular.ttf"
        )
        
        startActivityForResult?.launch(Intent(this, Liveness3DActivity::class.java).apply {
            putExtra(Liveness3DActivity.PARAM_LIVENESS3D_USER, liveness3DUser)
            putExtra(Liveness3DActivity.PARAM_FONTS, fontsFromAssets)
        })
```

Também foi implementado um novo retorno para caso o path da fonte ou o resource não seja encontrado `INVALID_FONT_PARAMS`.
