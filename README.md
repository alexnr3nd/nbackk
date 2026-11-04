# N-Back Offline (Android)

Projeto Android pronto para build pelo GitHub Actions. O app usa uma página HTML local dentro de um WebView; não carrega páginas externas e não precisa de conta, Google Play Services ou conexão com a internet para jogar.

## Gerar o APK pelo GitHub (usando apenas o celular)

1. Baixe e descompacte `NBackOffline-Android.zip`.
2. No GitHub, crie um repositório novo (por exemplo `nback-offline`).
3. Envie **todos os arquivos e pastas que estão dentro** desta pasta para a raiz do repositório. É importante que `.github/workflows/android.yml` também seja enviado. No app do GitHub/site móvel, pode ser mais fácil usar a opção de enviar arquivos pelo navegador em modo computador.
4. Abra a aba **Actions** do repositório.
5. Se aparecer uma solicitação, permita executar GitHub Actions.
6. Aguarde o workflow **Build Android APK** terminar com marca verde.
7. Abra a execução concluída, desça até **Artifacts** e baixe `NBackOffline-debug-apk`.
8. Extraia o ZIP baixado. Dentro estará `app-debug.apk`. Abra-o no Android e autorize a instalação pelo navegador/gerenciador de arquivos, se solicitado.

Também é possível iniciar manualmente em **Actions → Build Android APK → Run workflow**.

## Build local

Requer JDK 17 e Gradle 8.9+:
```bash
gradle assembleDebug
```
APK: `app/build/outputs/apk/debug/app-debug.apk`

## O que está no projeto

- `app/src/main/assets/index.html`: interface e mecânica do treino.
- `MainActivity.java`: contêiner Android e importação/exportação de backup pelo seletor de arquivos do sistema.
- `.github/workflows/android.yml`: build automático e publicação do APK como artifact.

## Privacidade e limitações atuais

- O Manifest não declara permissão `INTERNET`.
- Histórico e recordes são mantidos no armazenamento local do WebView.
- Backup exportado como TXT contém JSON para poder ser restaurado.
- A versão atual é uma implementação própria inspirada no formato N-Back; não é uma cópia exata do aplicativo de referência.
- O APK gerado pelo workflow é **debug**, adequado para instalar e testar. Para publicar na Play Store ou distribuir como release assinado, é necessário configurar uma chave de assinatura.
