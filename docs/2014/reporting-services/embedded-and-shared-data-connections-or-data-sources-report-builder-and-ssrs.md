---
title: Inseridos e compartilhados, conexões de dados ou fontes de dados (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf9b9bfd500c5ddb9e10fb1e2320bf0287114808
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934492"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>Conexões de dados ou fontes de dados compartilhadas e inseridas (Construtor de Relatórios e SSRS)
  Os relatórios usam conexões de dados para recuperar dados de um relatório quando uma consulta é executada ou o relatório é processado. Você escolhe em uma lista de tipos de conexões de dados internos a serem conectados a um banco de dados relacional, a um banco de dados multidimensional, a um serviço Web ou a alguma outra fonte de dados. Os termos a seguir são usados para descrever conexões de dados.  
  
-   **Conexão de dados.** Também conhecida como uma *fonte de dados*. Uma conexão de dados inclui um nome e propriedades de conexão que dependem do tipo de conexão. Por design, uma conexão de dados não inclui credenciais. Uma conexão de dados não especifica os dados a serem recuperados da fonte de dados externa. Para fazer isso, especifique uma consulta ao criar um conjunto de dados.  
  
-   **Definição da fonte de dados.** Um arquivo que contém a representação XML de uma fonte de dados de relatório. Quando um relatório é publicado, suas fontes de dados são salvas no servidor de relatório ou no site do SharePoint como definições de fonte de dados, independentemente da definição de relatório. Por exemplo, um administrador de servidor de relatório poderia atualizar a cadeia de conexão ou credenciais. Em um servidor de relatório nativo, o tipo de arquivo é .rds. Em um site do SharePoint, o tipo de arquivo é .rsds.  
  
-   **Cadeia de conexão.** Uma cadeia de conexão é uma versão de cadeia de caracteres das propriedades de conexão necessárias à conexão a uma fonte de dados. As propriedades de conexão variam com base no tipo de conexão de dados. Para obter exemplos, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
-   **Fonte de dados compartilhadas.** Uma fonte de dados disponível em um servidor de relatório ou site do SharePoint a ser usada por vários relatórios.  
  
-   **Fonte de dados inserida** Também conhecida como uma *Fonte de dados específica de relatório*. Uma fonte de dados que é definida em um relatório e é usada apenas por esse relatório.  
  
-   **Credenciais.** Credenciais são as informações de autenticação a serem fornecidas para permitir que você acesse dados externos.  
  
 A diferença entre as fontes de dados inseridas e compartilhadas está em como elas são criadas, armazenadas e gerenciadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>Fontes de dados compartilhadas  
 As fontes de dados compartilhadas são úteis quando você usa fontes de dados frequentemente. É recomendado usar fontes de dados compartilhadas o máximo possível. Elas facilitam o acesso e o gerenciamento dos relatórios, além de ajudar a proteger os relatórios e as fontes de dados acessados. Se precisar de uma fonte de dados compartilhada, peça ao administrador do sistema para criar uma para você.  
  
 No Construtor de Relatórios, não é possível criar uma fonte de dados compartilhada. Você pode navegar do servidor de relatório até uma fonte de dados compartilhada e selecioná-la. Para obter mais informações, consulte [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 No Designer de Relatórios, não é possível navegar até uma fonte de dados compartilhada no servidor de relatório. No Gerenciador de Soluções, você pode criar fontes de dados compartilhados como parte de um projeto e decidir se deve implantá-las em um servidor de relatório. Talvez você opte por usá-las localmente apenas por causa das diferenças em credenciais exigidas pelo seu computador ou pelo servidor de relatório. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 O seguinte ícone indica um item fonte de dados compartilhada na hierarquia da pasta do servidor de relatório: ![Ícone Fonte de dados compartilhada](media/hlp-16datasource.png "Ícone Fonte de dados compartilhada")  
  
## <a name="embedded-data-sources"></a>Fontes de dados inseridas  
 Uma fonte de dados inserida é uma conexão de dados salva na definição de relatório. As informações de conexão de fonte de dados inserida só podem ser usadas pelo relatório no qual a fonte de dados está inserida. Para definir e gerenciar fontes de dados inseridas, use a caixa de diálogo **Propriedades da Fonte de Dados** .  
  
##  <a name="Comparing"></a> Comparando incorporados e fontes de dados compartilhadas  
 A tabela seguinte resume as diferenças entre fontes de dados inseridas e compartilhadas:  
  
|Descrição|Inserida<br /><br /> fonte de dados|Compartilhado<br /><br /> fonte de dados|  
|-----------------|------------------------------|----------------------------|  
|A conexão de dados é inserida na definição do relatório.|![Disponível](media/greencheck.gif "Disponível")||  
|O ponteiro para a conexão de dados no servidor de relatório é inserido na definição do relatório.||![Disponível](media/greencheck.gif "Disponível")|  
|Gerenciada no servidor de relatório|![Disponível](media/greencheck.gif "Disponível")|![Disponível](media/greencheck.gif "Disponível")|  
|Obrigatória para conjuntos de dados compartilhados||![Disponível](media/greencheck.gif "Disponível")|  
|Obrigatória para componentes||![Disponível](media/greencheck.gif "Disponível")|  
  
## <a name="data-source-credentials"></a>Credenciais da fonte de dados  
 As credenciais são usadas para criar uma fonte de dados inserida, para executar uma consulta ou para recuperar dados durante o processamento de relatórios. O proprietário da fonte de dados determina o tipo de credenciais que você deve usar para acessar os dados. As credenciais são gerenciadas independentemente da conexão de dados em um servidor de relatório, em um site do SharePoint ou em um computador local em um ambiente de criação de relatório. Dependendo do tipo de fonte de dados, as credenciais podem ser salvas para evitar a solicitação ou podem ser definidas para solicitar o acesso de cada usuário. As credenciais de que você precisa variam de acordo com a origem da conexão à fonte de dados: do computador ou do servidor de relatório. Para obter mais informações, consulte [especificar as credenciais no construtor de relatórios](../../2014/reporting-services/specify-credentials-in-report-builder.md) e [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Conceitos de criação de relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
