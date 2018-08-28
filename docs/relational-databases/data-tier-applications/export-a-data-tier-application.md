---
title: Exportar um aplicativo da camada de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.exportdac.progress.f1
- sql13.swb.exportdac.summary.f1
- sql13.swb.exportdac.results.f1
- sql13.swb. exportdac.results.f1
- sql13.swb. exportdac.summary.f1
- sql13.swb. exportdac.settings.f1
- sql13.swb.exportdac.welcome.f1
- sql13.swb.exportdac.settings.f1
helpviewer_keywords:
- How to [DAC], export
- wizard [DAC], export
- export DAC
- data-tier application [SQL Server], export
ms.assetid: 61915bc5-0f5f-45ac-8cfe-3452bc185558
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f4f5e1eaf2632b25bdbc44a5cdd5eec3dde28b5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43100160"
---
# <a name="export-a-data-tier-application"></a>Exportar um aplicativo da camada de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A exportação de um aplicativo de camada de dados implantado (DAC) ou de um banco de dados cria um arquivo de exportação que contém as definições dos objetos no banco de dados e todos os dados contidos nas tabelas. O arquivo de exportação pode ser importado para outra instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], ou para [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. As operações de importação-exportação podem ser combinadas para migrar um DAC entre instâncias, criar um arquivo morto ou criar uma cópia local de um banco de dados implantado no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="before-you-begin"></a>Antes de começar  
 O processo de exportação compila um arquivo de exportação DAC em duas fases.  
  
1.  A exportação compila uma definição de DAC no arquivo de exportação – BACPAC– do mesmo modo que uma extração de DAC compila uma definição de DAC em um arquivo de pacote de DAC. A definição do DAC exportada inclui todos os objetos no banco de dados atual. Se o processo de exportação for executado em um banco de dados que foi implantado originalmente de um DAC, e tiverem sido feitas alterações diretamente no banco de dados depois da implantação, a definição exportada corresponderá ao objeto definido no banco de dados, e não ao que foi definido no DAC original.  
  
2.  A exportação em massa copia os dados de todas as tabelas no banco de dados e incorpora os dados no arquivo de exportação.  
  
 O processo de exportação define a versão de DAC como 1.0.0.0 e a descrição de DAC no arquivo de exportação para uma cadeia de caracteres vazia. Se o banco de dados foi implantado de um DAC, a definição do DAC no arquivo de exportação conterá o nome atribuído ao DAC original; caso contrário, o nome do DAC será definido como o nome do banco de dados.  
  

###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Um DAC ou banco de dados só pode ser exportado de um banco de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior.  
  
 Você não poderá exportar um banco de dados com objetos sem suporte em um DAC ou usuários contidos. Para obter mais informações sobre os tipos de objetos com suporte em um DAC, consulte [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="Permissions"></a> Permissões  
 A exportação de um DAC exige, no mínimo, as permissões ALTER ANY LOGIN e VIEW DEFINITION do escopo do banco de dados, bem como as permissões SELECT em **sys.sql_expression_dependencies**. A exportação de um DAC pode ser feita por membros da função de servidor fixa securityadmin que também são membros da função de banco de dados fixa database_owner no banco de dados do qual o DAC é exportado. Membros da função de servidor fixa sysadmin ou da conta interna do administrador do sistema do SQL Server denominada **sa** também podem exportar um DAC.  
  
##  <a name="UsingDeployDACWizard"></a> Usando o Assistente para Exportar Aplicativo da Camada de Dados  
 **Para exportar um DAC usando um assistente**  
  
1.  Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seja no local ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  No **Pesquisador de Objetos**, expanda o nó da instância na qual você deseja exportar o DAC.  
  
3.  Clique com o botão direito do mouse no nome do banco de dados.  
  
4.  Clique em **Tarefas** e selecione **Exportar Aplicativo da Camada de Dados...**  
  
5.  Conclua as etapas das caixas de diálogo do assistente:  
  
    -   [Página de Introdução](#Introduction)  
  
    -   [Página Configurações de Exportação](#Export_settings)  
  
    -   [Página de Validação](#Validation)  
  
    -   [Página de Resumo](#Summary)  
  
    -   [Página Progresso](#Progress)  
  
    -   [Página Resultados](#Results)  
  
##  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas do Assistente de Exportação do Aplicativo da Camada de Dados.  
  
 **Opções**  
  
 **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página de Introdução no futuro.  
  
 **Avançar** – Segue para a página **Selecionar Pacote de DAC** .  
  
 **Cancelar** – Cancela a operação e fecha o Assistente.  
  
##  <a name="Export_settings"></a> Página Configurações de Exportação  
 Use essa página para especificar o local onde criar o arquivo BACPAC a ser criado.  
  
-   **Salvar no disco local** – Cria um arquivo BACPAC em um diretório no computador local. Clique em **Procurar…** para navegar no computador local ou especifique o caminho no espaço fornecido. O nome do caminho deve incluir um nome de arquivo e a extensão .bacpac.  
  
-   **Salvar no Microsoft Azure** – Cria um arquivo BACPAC em um contêiner do Microsoft Azure. Você deve se conectar a um contêiner do Windows Azure para validar esta opção. Observe que esta opção também exige que você especifique um diretório local para o arquivo temporário. Observe que o arquivo temporário será criado no local especificado e permanecerá lá depois que a operação for concluída.  
  
 Para especificar um subconjunto de tabelas a serem exportadas, use a opção **Avançado** .  
  
##  <a name="Validation"></a> Página de Validação  
 Use a página de validação para revisar os problemas que bloqueiam a operação. Para continuar, resolva os problemas de bloqueio e clique em **Executar Novamente a Validação** para verificar se a validação foi bem-sucedida.  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Summary"></a> Página de Resumo  
 Use esta página para analisar a origem especificada e as configurações de destino para a operação. Para concluir a operação de exportação usando as configurações especificadas, clique em **Concluir**. Para cancelar a operação de exportação e sair do Assistente, clique em **Cancelar**.  
  
##  <a name="Progress"></a> Página Progresso  
 Esta página exibe a barra de progresso que indica o status da operação. Para exibir o status detalhado, clique na opção **Exibir detalhes** .  
  
##  <a name="Results"></a> Página Resultados  
 Esta página reporta o êxito ou falha da operação de exportação, mostrando os resultados de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Clique no link para exibir um relatório do erro para essa ação.  
  
 Clique em **Concluir** para fechar o Assistente.  
  
##  <a name="NetApp"></a> Usando um aplicativo .NET Framework  
 **Para exportar um DAC usando o método Export() em um aplicativo .NET Framework.**  
  
 Para exibir um exemplo de código, baixe o aplicativo de exemplo do DAC em [Codeplex](http://go.microsoft.com/fwlink/?LinkId=219575)  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o DAC a ser exportado.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Use o método **Export** do tipo **Microsoft.SqlServer.Management.Dac.DacStore** para exportar o DAC. Especifique o nome do DAC a ser exportado e o caminho para a pasta onde o arquivo de exportação será colocado.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Extrair um DAC de um banco de dados](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)  
  
  
