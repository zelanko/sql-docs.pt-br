---
title: Extrair um DAC de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.extractdacwizard.buildandsave.f1
- sql12.swb.extractdacwizard.setdacproperties.f1
- sql12.swb.extractdacwizard.validationandsummary.f1
- sql12.swb.extractdacwizard.introduction.f1
- sql12.swb.extractdacwizard.selectdatapage.f1
helpviewer_keywords:
- extract DAC
- How to [DAC], extract
- data-tier application [SQL Server], extract
- wizard [DAC], extract
ms.assetid: ae52a723-91c4-43fd-bcc7-f8de1d1f90e5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37bb440288ccbc832d89180855566a969830e2ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797990"
---
# <a name="extract-a-dac-from-a-database"></a>Extrair um DAC de um banco de dados
  Use o **Assistente para Extrair um Aplicativo da Camada de Dados** ou um script do Windows PowerShell para extrair um pacote de DAC (aplicativo da camada de dados) de um banco de dados do SQL Server existente. O processo de extração cria um arquivo de pacote de DAC que contém definições dos objetos de banco de dados e os elementos em nível de instância relacionados. Por exemplo, um arquivo de pacote de DAC contém as tabelas do banco de dados, os procedimentos armazenados, as exibições e os usuários junto com os logons que mapeiam para os usuários de banco de dados.  
  
-   **Antes de começar:**  [limitações e restrições](#LimitationsRestrictions), [permissões](#Permissions)  
  
-   **Para extrair um DAC, usando:**  [o assistente para extrair aplicativo da camada de dados](#UsingDACExtractWizard), [PowerShell](#ExtractDACPowerShell)  
  
## <a name="before-you-begin"></a>Antes de começar  
 É possível extrair um DAC de bancos de dados que residam em instâncias do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 4 ou posterior. Se o processo de extração for executado em um banco de dados que foi implantado de um DAC, só serão extraídas as definições dos objetos no banco de dados. O processo não faz referência ao DAC registrado no `msdb` (**Master** in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). O processo de extração não registra a definição do DAC na instância atual do Mecanismo de Banco de Dados. Para obter mais informações sobre como registrar um DAC, consulte [Register a Database As a DAC](register-a-database-as-a-dac.md).  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Um DAC só pode ser extraído de um banco de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior. Você não poderá extrair um DAC se o banco de dados tiver objetos que não tenham suporte em um DAC ou usuários contidos. Para obter mais informações sobre os tipos de objetos com suporte em um DAC, consulte [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="Permissions"></a> Permissões  
 A extração de um DAC exige, pelo menos, as permissões ALTER ANY LOGIN e VIEW DEFINITION do escopo do banco de dados, bem como as permissões SELECT em **sys.sql_expression_dependencies**. A extração de um DAC pode ser feita por membros da função de servidor fixa securityadmin que também são membros da função de banco de dados fixa database_owner no banco de dados do qual o DAC é extraído. Membros da função de servidor fixa sysadmin ou a conta interna do administrador do sistema do SQL Server chamada **sa** também podem extrair um DAC.  
  
##  <a name="UsingDACExtractWizard"></a> Usando o Assistente para Extrair um Aplicativo da Camada de Dados  
 **Para extrair um DAC usando um assistente**  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o banco de dados do qual o DAC será extraído.  
  
2.  Expanda o nó **Bancos de Dados** .  
  
3.  Clique com o botão direito do mouse no nó do banco de dados do qual o DAC é extraído, aponte para **Tarefas** e selecione **Extrair Aplicativo da Camada de Dados...**  
  
4.  Conclua as etapas das caixas de diálogo do assistente:  
  
    1.  [Página de Introdução](#Introduction)  
  
    2.  [página Selecionar Dados](#SelectData)  
  
    3.  [Página Definir Propriedades](#SetProperties)  
  
    4.  [Página Validação e Resumo](#ValidateSummary)  
  
    5.  [Página Criar Pacote](#BuildPackage)  
  
###  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas para extrair um aplicativo da camada de dados.  
  
 **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página no futuro.  
  
 **Avançar >** : continua para a página **Escolher Método**.  
  
 **Cancelar** – Encerra o assistente sem extrair um aplicativo da camada de dados do banco de dados.  
  
###  <a name="SelectData"></a>Página selecionar dados  
 Use esta página do assistente para selecionar os dados de referência que você deseja incluir em seu arquivo de pacote de DAC (aplicativo da camada de dados). A inclusão de dados em seu pacote de DAC é opcional. O pacote de DAC já incluirá o esquema de todos os objetos de banco de dados com suporte e objetos de instância relacionados a seu banco de dados.  
  
 Você pode incluir até 10 MB de dados de referência em seu arquivo de pacote de DAC. No entanto, para que tabelas sejam incluídas no DAC, elas não podem conter tipos de dados BLOB (objeto binário grande) como **image** ou **varchar(max)** . Para extrair quantidades maiores de dados para transferência para outro banco de dados, use o SQL Server Integration Services, o utilitário de cópia em massa ou um das muitas outras técnicas de migração de dados.  
  
 **Tabela de banco de dados** – Marque a caixa de seleção ao lado das tabelas do banco de dados que contêm os dados que você deseja incluir em seu pacote de DAC. Você pode selecionar até dez tabelas com mais ou menos 10.000 linhas.  
  
###  <a name="SetProperties"></a>Página definir propriedades  
 Use esta página do assistente para descrever o aplicativo da camada de dados (DAC). Estas propriedades são usadas para identificar o DAC e ajudam a distingui-lo de outros.  
  
 **Nome** – Este nome identifica o DAC. Pode ser diferente do nome do arquivo de pacote de DAC e deve descrever seu aplicativo. Por exemplo, se o banco de dados for usado para um aplicativo de finanças, você poderá nomeá-lo como Finanças do DAC.  
  
 **Versão (use xx.xx.xx.xx, em que x é um número)** – Um valor numérico que identifica a versão do DAC. A versão do DAC é usada no Visual Studio para identificar a versão do DAC em que os desenvolvedores estão trabalhando. Ao implantar um DAC, a versão é armazenada no banco `msdb` de dados e, posteriormente, pode ser exibida no nó aplicativos da camada [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]de **dados** no.  
  
 **Descrição:** – Opcional. Descreve o DAC. Ao implantar um DAC, a descrição é armazenada no banco `msdb` de dados e, posteriormente, pode ser exibida no nó **aplicativos da camada data** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Salvar o arquivo de pacote de DAC (inclua a extensão .dacpac no nome do arquivo):** – Salva o DAC em um arquivo de pacote de DAC, com uma extensão .dacpac. Clique no botão **Procurar** para especificar um nome e um local para o arquivo.  
  
 **Substituir o arquivo existente** – Marque esta caixa de seleção para substituir o arquivo do pacote de DAC se já existir um com o mesmo nome.  
  
###  <a name="ValidateSummary"></a>Página validação e Resumo  
 Nesta página, o assistente valida se todos os objetos de banco de dados têm suporte de um DAC (aplicativo da camada de dados). Também verifica dependências entre objetos de banco de dados para determinar o conjunto de objetos que podem ser incluídos com êxito no DAC. Depois disso, exibe o relatório de validação e resume as opções que você selecionou neste assistente. Para alterar uma opção, clique em **Anterior**. Para iniciar a extração de um DAC, clique em **Avançar**.  
  
> [!NOTE]  
>  Se um ou mais objetos não tiverem suporte de um DAC, o botão **Avançar** será desabilitado e o processo de extração talvez não continue. Nesses casos, é recomendável remover os objetos sem suporte e, em seguida, executar esse assistente novamente.  
  
 **Resumo** – Um resumo das opções que você selecionou é listado em **Propriedades do DAC**. Os resultados da validação são listados em **Objetos do DAC**. Há três tipos de resultados da validação:  
  
-   **Objetos incluídos no DAC com êxito**: estes objetos e suas dependências têm suporte e podem ser incluídos com êxito no DAC.  
  
-   **Objetos incluídos no DAC com avisos**: estes objetos têm suporte, mas dependem de outros objetos que não têm suporte em um DAC.  
  
-   **Objetos não incluídos no DAC**: estes objetos não têm suporte e devem ser removidos do banco de dados antes da extração bem-sucedida de um DAC.  
  
 O processo de validação verifica vários níveis de dependências. Por exemplo, se um procedimento armazenado depender de uma tabela que usa o tipo de dados de CLR não tiver suporte, o procedimento armazenado será listado em **Objetos incluídos no DAC com avisos**.  
  
 Se um ou mais objetos não tiverem suporte de um DAC, o botão **Avançar** será desabilitado e o processo de extração não continuará. Nesses casos, é recomendável remover os objetos que não têm suporte e, em seguida, executar esse assistente novamente.  
  
 **Salvar Relatório** – Permite salvar um arquivo baseado em HTML que lista todos os objetos no nó **Objetos do DAC** no resumo. Esse relatório pode ser útil quando alguns de seus objetos de banco de dados não têm suporte em um DAC. Use o relatório para alterar ou remover objetos que não têm suporte, antes de tentar extrair o DAC novamente.  
  
###  <a name="BuildPackage"></a>Página Criar pacote  
 Use esta página para monitorar o andamento do assistente enquanto ele extrai o aplicativo da camada de dados (DAC).  
  
 **Ação** – Durante a ação **Criar e salvar arquivo de pacote de DAC** , o assistente extrai um DAC do banco de dados SQL Server. Em seguida, o pacote de DAC é criado na memória e salvo no local especificado. Clique nos links na coluna **Resultado** para ver o resultado da etapa correspondente.  
  
 **Salvar Relatório** – Clique para salvar os resultados do progresso do assistente em um arquivo.  
  
 **Concluir** – Clique para fechar o assistente após a conclusão do processamento, ou se ocorrer um erro.  
  
##  <a name="ExtractDACPowerShell"></a>Extrair um DAC usando o PowerShell  
 **Para extrair um DAC de um banco de dados usando o método Extract() em um script do PowerShell**  
  
1.  Crie um objeto do Servidor SMO e defina-o como a instância que contém o banco de dados do qual o DAC será extraído.  
  
2.  Adicione uma variável que especifique o nome do banco de dados.  
  
3.  Especifique os metadados do DAC, como o nome, a versão e a descrição do DAC.  
  
4.  Especifique o caminho completo e o nome de arquivo do arquivo de pacote de DAC extraído.  
  
5.  Execute o método Extract com as informações especificadas acima.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir extrai um DAC denominado MyApplication de um banco de dados denominado MyDB.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Specify the database to extract to a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Specify the location and name for the extracted DAC package.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
  
## Extract the DAC.  
$extractionunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$extractionunit.Description = $description  
$extractionunit.Extract($dacpacPath)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da camada de dados](data-tier-applications.md)  
