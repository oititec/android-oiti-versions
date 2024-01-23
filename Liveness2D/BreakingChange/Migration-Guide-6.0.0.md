# Migration Guide - 6.0.0

Este guia apresenta orientações detalhadas sobre as mudanças significativas introduzidas na versão 6.0.0 do Liveness 2D da Oiti. Siga todas as etapas abaixo para garantir uma atualização assertiva e uma transição suave para a nova versão da nossa SDK.

# Atualizações Importantes

## Remoção do Parâmetro `PARAM_ENDPOINT`

Na versão 6.0.0, o parâmetro `PARAM_ENDPOINT` foi removido na Activity e substituído pelo `PARAM_ENVIRONMENT`.

- **Environment.HML** para ambiente de homologação.
- **Environment.PRD** para ambiente de produção.

```kotlin
   putExtra(FaceCaptchaActivity.PARAM_ENVIRONMENT, Environment.HML)
```

#### Alterações Necessárias

Se sua aplicação utiliza o parâmetro `PARAM_ENDPOINT`, atualize seu código para utilizar o novo parâmetro `PARAM_ENVIRONMENT` conforme necessário.

## Nova Forma de Customização de Cores e Fontes

Introduzimos uma nova forma de customização de cores e fontes para plataformas híbridas, caso o `PARAM_HYBRID` seja `true`, e para setar a customização criamos um builder e passamos no parâmetro `PARAM_THEME`.

```kotlin
    putExtra(DocumentscopyActivity.PARAM_THEME, getNewTheme())
```

```kotlin
    private fun getNewTheme() = DocCopyTheme.Builder()

        // NewCustom Instruction
        .instructionBackButtonIcon(R.drawable.cancel_button)
        .instructionTitleText("Aro aqui eu To")
        .instructionTitleColor("#A5CD39")
        .instructionCaptionColor("#A5CD39")
        .instructionCaptionText("123 mais um teste")
        .instructionBackgroundColor("#A5CD39")
        .instructionBottomSheetBackgroundColor("#333333")


        //Options Icons Colors
        .setInstructionOptionDocumentIconColor("#A5CD39")
        .setInstructionOptionLightingIconColor("#fc0000")
        //Options Sphere Border/background Colors
        .setInstructionOptionDocumentBorderColor("#fc0000")
        .setInstructionOptionDocumentBackgroundColor("#0E1979")
        .setInstructionOptionLightingBorderColor("#fc0000")
        .setInstructionOptionLightingBackgroundColor("#A5CD39")

        //Options Texts
        .setInstructionOptionDocumentTextColor("#A5CD39")
        .setInstructionOptionDocumentTextFont("ubuntu_regular")
        .setInstructionOptionLightingTextColor("#A5CD39")
        .setInstructionOptionLightingTextFont(R.font.ubuntu_regular)

        .setInstructionOptionDocumentText("title Oneee")
        .setInstructionOptionLightingText("title Twoo")

        //Continue Button
        .setInstructionContinueButtonBackgroundColor("#FFFFFF")
        .setInstructionContinueButtonTextColor("#A5CD39")
        .setInstructionContinueButtonTextFont(R.font.ubuntu_regular)

        .build()
```

#### Atualização na Lógica de Customização

Se você personaliza cores e fontes para plataformas híbridas, ajuste sua lógica de customização para incorporar a nova abordagem.

## Implementação do Koin para Injeção de Dependências

A partir da versão 6.0.0, implementamos o Koin para injeção de dependências.

### Nova Tela de Instruções

`PARAM_CUSTOM_HOME_FRAGMENT` parâmetro para passar o XML da tela de instruções customizadas.

Introduzimos uma nova tela de instruções com os componentes e ids obrigatórios:
`@+id/contentView` `<ConstraintLayout />`, `@+id/backButton` `<ImageButton />`, `@+id/backButton` `<ImageButton />`, `@+id/continueButton` `<AppCompatButton />,` `@+id/activityIndicatorView` `<ProgressBar />`

Exemplo de tela customizada:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/white"
    android:padding="32dp">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/contentView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <TextView
            android:id="@+id/infoTextView"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:gravity="center_horizontal"
            android:text="@string/fc_doc_home_subtitle"
            android:textColor="@color/dark_text"
            android:textSize="16sp"
            app:layout_constraintBottom_toTopOf="@id/cnhPictureButton"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintVertical_chainStyle="packed" />

        <ImageButton
            android:id="@+id/backButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="16dp"
            android:layout_marginLeft="16dp"
            android:layout_marginTop="8dp"
            android:background="@null"
            android:padding="16dp"
            android:src="@drawable/fc_arrow_left"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />


        <androidx.appcompat.widget.AppCompatButton
            android:id="@+id/continueButton"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="32dp"
            android:background="@color/custom_blue"
            android:text="Continue Button"
            android:textColor="@android:color/white"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@id/backButton" />

    </androidx.constraintlayout.widget.ConstraintLayout>

    <ProgressBar
        android:id="@+id/activityIndicatorView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### Adição de Funcionalidades de Device

Na versão 6.0.0, foram adicionadas as seguintes funcionalidades de Device:

- Device Intelligence
- Device Behavior
- Device Location
- Device Info

### Adicionar Permissão de Localização

Para utilizar a funcionalidade de captura de localização, é necessário adicionar a seguinte permissão em seu AndroidManifest.xml:

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```
