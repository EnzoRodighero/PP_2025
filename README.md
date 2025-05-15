PROBLEMA COM ARQUIVOS .resx BLOQUEADOS APÓS BAIXAR O PROJETO

Descrição:
-----------
Ao clonar ou baixar este projeto do GitHub, é possível que você encontre o seguinte erro ao tentar compilar ou executar no Visual Studio:

Couldn't process file Views\Frm.resx due to its being in the Internet or Restricted zone or having the mark of the web on the file.
Couldn't process file Views\FrmPrincipal.resx due to its being in the Internet or Restricted zone or having the mark of the web on the file.

Esse erro acontece porque o Windows aplica uma marca de segurança chamada "Mark of the Web" (MOTW) em arquivos baixados da internet. Essa marca impede que o Visual Studio processe corretamente arquivos como .resx, .csproj e outros.

Como resolver:
--------------

Opção 1: Desbloquear manualmente pelo Windows Explorer

1. Navegue até a pasta onde está o projeto.
2. Clique com o botão direito sobre a pasta do projeto.
3. Vá em "Propriedades".
4. Se aparecer a mensagem "Este arquivo veio de outro computador e pode estar bloqueado", marque a opção "Desbloquear".
5. Clique em "Aplicar" e depois em "OK".

Dica: Esse método pode não aparecer dependendo das configurações do sistema. Se isso acontecer, use o PowerShell.

Opção 2: Desbloquear todos os arquivos usando PowerShell

1. Abra o PowerShell na pasta raiz do projeto.
   Dica: Segure SHIFT e clique com o botão direito na pasta do projeto, depois escolha "Abrir no PowerShell aqui".
2. Execute o seguinte comando:

   Get-ChildItem -Recurse | Unblock-File

Esse comando remove a marca da web de todos os arquivos e subpastas do projeto.

Verificação (opcional):
-----------------------
Para verificar se ainda existem arquivos bloqueados, você pode rodar o comando abaixo:

   Get-ChildItem -Recurse | Where-Object { $_.Attributes -match "Blocked" }

Se não retornar nada, então todos os arquivos estão desbloqueados.

Depois de desbloquear:
-----------------------

- Feche o Visual Studio (caso esteja aberto).
- Reabra o Visual Studio.
- Abra o projeto novamente.
- Compile ou execute.

Observações finais:
--------------------
- Sempre extraia o arquivo ZIP antes de abrir o projeto se ele foi baixado compactado.
- Se o projeto estiver dentro de uma pasta do OneDrive, Google Drive, etc., isso pode interferir nas permissões. Prefira pastas locais.
- 
