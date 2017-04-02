---
title: "Usar uma conex&#227;o de dados do Office (.odc) com relat&#243;rios (Reporting Services no modo integrado do SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "arquivos .odc (conexão de dados do Office)"
  - "integração com o SharePoint [Reporting Services], fontes de dados compartilhadas"
  - "arquivos .odc"
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Usar uma conex&#227;o de dados do Office (.odc) com relat&#243;rios (Reporting Services no modo integrado do SharePoint)
  Em cenários limitados, você pode usar um arquivo de conexão de dados do Office (.odc) para fornecer informações sobre conexão com um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Um arquivo .odc pode ser usado no lugar de um arquivo .rsds quando você cria uma fonte de dados compartilhados. O servidor de relatório usa um arquivo .odc do mesmo modo que usa um arquivo .rsds; ele lê o arquivo para detectar informações sobre tipo de fonte de dados, cadeia de caracteres de conexão e credenciais.  
  
 Nem todos os arquivos .odc podem ser usados com um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A extensão e as características do processamento de dados do relatório e do arquivo .odc determinam se este pode ser usado:  
  
-   O relatório deve ser criado para funcionar com um provedor de dados OLE DB ou ODBC. Se você tiver usado outra extensão de processamento de dados para criar o relatório, ele ou suas consultas poderão incluir recursos para os quais o provedor de dados OLE DB ou ODBC não ofereça suporte.  
  
-   O arquivo .odc deve ter a estrutura e os elementos esperados. As definições de provedor de dados e de credenciais devem ser definidas explicitamente no arquivo para que possam ser lidas pelo servidor de relatório. O melhor modo para definir esses valores é exportar o arquivo .odc antes de carregá-lo na biblioteca do SharePoint.  
  
-   O arquivo .odc deve especificar um tipo de conexão de OLE DB ou ODBC.  
  
-   O arquivo .odc deve especificar uma cadeia de caracteres de conexão.  
  
-   As credenciais podem ser definidas como **Nenhuma**, **Armazenada** ou **Integrada**. Se o método das credenciais for definido como **Armazenada**, o servidor de relatório solicitará que o usuário forneça credenciais, em vez de usar as armazenadas. O servidor de relatório não pode usar credenciais armazenadas conforme definido em um arquivo .odc.  
  
-   A fonte de dados deve ter esquema idêntico àquele usado para criar o relatório. Se as estruturas de dados diferirem, o relatório não será executado.  
  
-   O arquivo .odc deve ser criado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007 (versões mais antigas do .odc não são compatíveis com os arquivos de definição de relatórios).  
  
 Não é possível usar arquivos .odc que especifiquem conexões com fontes de dados que não possam ser processadas em um servidor de relatórios, mesmo que os tipos de fontes de dados .odc pareçam semelhantes a tipos que recebam suporte. Especificamente, se você tiver criado um arquivo .odc no Microsoft Excel 2007 que recupere dados do Microsoft Access, da Web ou de um arquivo de texto, não será possível usar esse arquivo .odc para fornecer dados a um relatório.  
  
 Os relatórios e modelos do Construtor de Relatórios não funcionam com arquivos .odc. Não é possível usar um arquivo .odc para gerar um modelo, nem configurar o modelo para usar uma fonte de dados compartilhados que esteja vinculada a um arquivo .odc.  
  
 Se você não estiver familiarizado com arquivos .odc, pode usar as instruções a seguir para criá-los e exportá-los. Um modo simples para criar um arquivo .odc para uma fonte de dados OLE DB é usar o Excel 2007 e o Assistente para Conexão de Dados. Observe que o assistente não cria uma fonte de dados; você deverá ter uma fonte de dados externa já definida.  
  
 Um arquivo .odc existente deve ser usado apenas se for totalmente compatível com o relatório e com as consultas. Se você encontrar erros que exijam modificações significativas no relatório ou no arquivo .odc, deverá criar um novo arquivo .rsds para o relatório. Para obter mais informações sobre como criar uma fonte de dados compartilhada que usa um arquivo .rsds, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md).  
  
### Para criar e exportar um arquivo .odc  
  
1.  Inicie o Excel 2007.  
  
2.  Na guia **Dados**, no grupo **Obter Dados Externos**, clique em **De Outras Fontes** e em **Do Assistente de Conexão de Dados**.  
  
3.  Selecione **Outros/Avançados** e clique em **Avançar**.  
  
4.  Selecione **Provedor do Microsoft OLE DB para SQL Server** e clique em **Avançar**.  
  
5.  Insira o nome do servidor (por padrão, esse é o nome de rede do computador) e uma conta de usuário que possua logon válido e permissões para banco de dados. Clique em **Avançar**.  
  
6.  Selecione um banco de dados e clique em **OK** para fechar a caixa de diálogo **Link de Dados**.  
  
7.  A caixa de seleção **Conectar à tabela específica** aparece marcada por padrão. Ela é usada para recuperar dados de uma tabela específica. O servidor de relatório ignora todas as consultas em um arquivo .odc; assim, o fato de essa caixa de seleção estar ou não marcada é irrelevante. As consultas que recuperam dados para um relatório são incluídas em um arquivo de definição de relatório, não em arquivos externos.  
  
8.  Enquanto a conexão permanecer aberta, você poderá editar propriedades e executar sua exportação. Na guia **Dados**, no grupo **Conexões**, clique em **Propriedades** e, então, no botão **Propriedades da Conexão** ao lado do nome da conexão.  
  
9. Na guia **Definição**, clique em **Exportar Arquivo de Conexão**.  
  
10. Insira o nome do arquivo e clique em **Salvar**. Feche o aplicativo e todos os arquivos abertos.  
  
### Para carregar e usar um arquivo .odc   
  
1.  Abra a biblioteca na qual você deseja carregar o arquivo de conexão.  
  
2.  No menu **Carregar**, clique em **Carregar documento**.  
  
3.  Clique em **Procurar**.  
  
4.  Selecione o arquivo .odc criado. Por padrão, o arquivo .odc está na pasta Meus Documentos, em Minhas Fontes de Dados.  
  
5.  Clique em **Abrir** para selecionar o arquivo e em **OK** para salvar a seleção. A página de propriedades relativa ao novo item é aberta automaticamente.  
  
6.  Em Tipo de Conteúdo, selecione **Fonte de Dados de Relatório** e, então, clique em **OK**.  
  
7.  Aponte para um relatório.  
  
8.  Clique na seta para baixo e selecione **Gerenciar Fontes de Dados**.  
  
9. Clique no nome da fonte de dados.  
  
10. Se o relatório usar informações sobre fontes de dados personalizadas, clique em **Compartilhado**.  
  
11. Em **Vínculo da Fonte de Dados**, clique no botão Procurar (**...**).  
  
12. Selecione o arquivo .odc recém-carregado.  
  
13. Clique em **OK** para selecionar o arquivo e em **OK** para salvar as alterações.  
  
     Se você estiver experimentando essas etapas com o banco de dados e os relatórios de exemplo do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], considere que somente o relatório Vendas da Empresa funcionará prontamente com um arquivo .odc. Os outros relatórios de amostra contêm parâmetros de consulta e recursos que não funcionam com o provedor do OLE DB. Entretanto, você pode fazer com que os relatórios funcionem com o provedor do OLE DB, se os modificar primeiramente no Designer de Relatórios.  
  
## Consulte também  
 [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  