---
title: Definir propriedades de fonte de dados (SSAS Multidimensional) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords: Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 732cdd40d8601f00854ebd6a3ebc3694f733e187
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>Definir propriedades da fonte de dados (SSAS multidimensional)
  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], um objeto de fonte de dados especifica uma conexão com um data warehouse externo ou um banco de dados relacional que fornece dados a um modelo multidimensional. As propriedades na fonte de dados determinam a cadeia de conexão, um intervalo de tempo limite, o número máximo de conexões e o nível de isolamento da transação.  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>Definir propriedades de fonte de dados no SQL Server Data Tools  
  
1.  Clique duas vezes em uma fonte de dados no Gerenciador de Soluções para abrir o Designer da Fonte de Dados.  
  
2.  Clique na guia **Informações sobre Representação** no Designer da Fonte de Dados. Para obter mais informações sobre a criação de uma fonte de dados, veja [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
## <a name="set-data-source-properties-in-management-studio"></a>Defina as propriedades da fonte de dados no Management Studio  
  
1.  Expanda a pasta do banco de dados, abra a pasta **Fonte de dados** sob o nome de banco de dados, clique com o botão direito do mouse em uma fonte de dados no **Pesquisador de Objetos** e selecione **Propriedades**.  
  
2.  Opcionalmente, modifique o nome, a descrição ou a opção de representação. Para obter mais informações, consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
## <a name="data-source-properties"></a>Propriedades de fonte de dados  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome, ID, Descrição**|Nome, ID e Descrição são usados para identificar e descrever o objeto de fonte de dados no modelo multidimensional.<br /><br /> Nome e Descrição poderão ser especificados no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] depois que você implantar ou processar a solução.<br /><br /> A ID é gerada quando o objeto é criado. Embora você possa modificar facilmente o nome e a descrição, IDs são somente leitura e não devem ser alteradas. Uma ID de objeto fixo preserva dependências de objeto e referências em todo o modelo.|  
|**Criar Carimbo de Data/Hora**|Essa propriedade somente leitura aparece no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Ela exibe a data e hora de criação da fonte de dados.|  
|**Última Atualização de Esquema**|Essa propriedade somente leitura aparece no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Ela exibe a data e a hora da última atualização dos metadados da fonte de dados. Este valor é atualizado quando você implanta a solução.|  
|**Tempo-limite da consulta**|Especifica quanto tempo uma solicitação de conexão será tentada antes de ser removida.<br /><br /> Digite o tempo limite da consulta no seguinte formato:<br /><br /> *\<Horas de >*:*\<minutos >*:*\<segundos >*<br /><br /> Essa propriedade pode ser substituída pela propriedade do servidor **DatabaseConnectionPoolTimeoutConnection** . Se a propriedade de servidor for menor, ela será usada em vez de **Tempo Limite da Consulta**.<br /><br /> Para obter mais informações sobre a propriedade **Tempo-limite da consulta** , consulte <xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>. Para obter mais informações sobre como definir esta propriedade de servidor, consulte [Propriedades OLAP](../../analysis-services/server-properties/olap-properties.md).|  
|**Cadeia de Conexão**|Especifica o local físico de um banco de dados que fornece dados para um modelo multidimensional e o provedor de dados usado para a conexão. Estas informações são fornecidas para uma biblioteca de cliente que faz a solicitação de conexão. O provedor determina quais propriedades podem ser definidas na cadeia de conexão.<br /><br /> A cadeia de conexão é criada usando as informações fornecidas na caixa de diálogo **Gerenciador de Conexões** . Você também pode exibir e editar a cadeia de conexão no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] na página de propriedades da fonte de dados.<br /><br /> Para um banco de dados do SQL Server, uma cadeia de conexão que contém **ID de usuário** indica a autenticação de banco de dados; uma conexão que contém **Integrated Security=SSPI** indica a autenticação do Windows.<br /><br /> Você pode alterar o servidor ou nome de banco de dados se o banco de dados tiver sido movido para um novo local. Verifique se as credenciais atualmente especificadas para a conexão são mapeadas para um logon de banco de dados.|  
|**Número máximo de conexões**|Especifica o número máximo de conexões permitido pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar à fonte de dados. Se forem necessárias mais conexões, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aguardará até que uma conexão fique disponível. O padrão é 10. Restringir o número de conexões garante que a fonte de dados externa não seja sobrecarregada com solicitações do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Isolamento**|Especifica o comportamento de bloqueio e controle de versão de linha das instruções de comandos SQL emitidos por uma conexão para um banco de dados relacional. Os valores válidos são ReadCommitted ou Snapshot. O padrão é ReadCommitted, que especifica que os dados devem ser confirmados antes de serem lidos, impedindo leituras sujas. O instantâneo especifica que as leituras são de um instantâneo de dados previamente confirmados. Para obter mais informações sobre o nível de isolamento no SQL Server, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).|  
|**Provedor Gerenciado**|Exibe o nome do provedor gerenciado, como System.Data.SqlClient ou System.Data.OracleClient, se a fonte de dados usar um provedor gerenciado.<br /><br /> Se a fonte de dados não usar um provedor gerenciado, essa propriedade exibirá uma cadeia de caracteres vazia.<br /><br /> Esta propriedade é somente leitura no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para alterar o provedor usado na conexão, edite a cadeia de conexão.|  
|**Informações sobre Representação**|Especifica a identidade do Windows sob a qual o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executado ao conectar-se a uma fonte de dados que usa a autenticação do Windows. As opções incluem usar um conjunto predefinido de credenciais do Windows, a conta de serviço, a identidade do usuário atual, ou uma opção herdada que pode ser útil se seu modelo contiver vários objetos de fonte de dados. Para obter mais informações, consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).<br /><br /> No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], a lista de valores válidos inclui estes valores:<br /><br /> **ImpersonateAccount** (use um nome de usuário e senha específicos do Windows para se conectar à fonte de dados).<br /><br /> **ImpersonateServiceAccount** (utilize a identidade de segurança da conta de serviço para se conectar à fonte de dados). Este é o valor padrão.<br /><br /> **ImpersonateCurrentUser** (utilize a identidade de segurança do usuário atual para se conectar à fonte de dados). Esta opção só é válida para consultas de mineração de dados que recuperam dados de um data warehouse ou banco de dados externo; não escolha-o para conexões de dados usadas para processamento, carregamento ou write-back em um banco de dados multidimensional.<br /><br /> **Herdar** ou **padrão** (use as configurações de representação do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém este objeto de fonte de dados). As propriedades de banco de dados incluem opções de representação.|  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
