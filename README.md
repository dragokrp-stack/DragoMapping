# Drago Mapping — Base do Projeto

Esta é a **primeira etapa** do app: estrutura Gradle + tema visual + navegação.
Ainda não inclui o motor de remapeamento funcional nem persistência de perfis
— isso vem nas próximas etapas (veja "Próximos passos" abaixo).

## Como abrir

1. Abra a pasta `DragoMapping/` no Android Studio (Koala ou mais recente).
2. Deixe o Android Studio gerar o Gradle Wrapper automaticamente na primeira
   sincronização (ele oferece isso sozinho; o wrapper binário não foi incluído
   aqui porque este ambiente não tem acesso à internet para baixá-lo).
3. Rode em um emulador ou dispositivo com **Android 10 (API 29) ou superior**.

## O que já está pronto

- Projeto Gradle (Kotlin + Jetpack Compose), `minSdk 29`, suporte declarado a
  celular, tablet, Android TV/Google TV (`LEANBACK_LAUNCHER`) e Samsung DeX.
- Tema visual preto/roxo com **3 variações**: Escuro, Claro e AMOLED
  (`ui/theme/Theme.kt`), trocável em tempo real pela tela de Ajustes.
- Navegação principal com 5 seções: Painel, Perfis, Teclado, Mouse, Ajustes.
- Textos em **português (padrão), inglês e espanhol** (`res/values*/strings.xml`).
- `AndroidManifest.xml` já declarando, de forma comentada e transparente,
  todas as permissões que os recursos avançados vão exigir (Accessibility
  Service, overlay, Bluetooth, USB host, etc.) — nada é solicitado ainda em
  runtime, isso entra junto com cada recurso.
- Esqueleto do `RemapAccessibilityService` (declarado no manifesto e no XML
  de configuração), pronto para receber a lógica de captura de teclado.

## Limitações técnicas importantes (para você já saber)

- Remapeamento de teclado/mouse **dentro de jogos em tela cheia** tem limites
  reais no Android sem root — o Accessibility Service funciona bem para apps
  em geral, mas alguns jogos capturam input diretamente.
- **Polling rate** não é algo configurável via software por um app; no máximo
  é possível *exibir* a taxa reportada pelo periférico.
- Importação de perfis **reWASD**: o formato deles é proprietário/não
  documentado. Vamos construir um conversor "melhor esforço" — não uma
  engenharia reversa completa do formato deles.

## Próximos passos sugeridos

1. `ProfileRepository` — modelo de dados + salvar/carregar perfis (DataStore/JSON).
2. Import/export de perfis (formato próprio `.dmap` em JSON) + conversor best-effort de arquivos reWASD.
3. `RemapAccessibilityService` funcional — captura real de teclas.
4. `InputEngine` para mouse/controle (DPI virtual, curva de resposta, deadzone).
5. Editor visual de teclas (drag-and-drop).
