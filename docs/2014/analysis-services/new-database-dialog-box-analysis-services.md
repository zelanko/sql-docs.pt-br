---
title: Caixa de diálogo novo banco de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df7d3eb279fdde62e97204b17e81420382ca62fa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191267"
---
# <a name="new-database-dialog-box-analysis-services"></a>Caixa de diálogo Novo Banco de Dados (Analysis Services)
  Use a caixa de diálogo **Novo Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para criar um novo banco de dados vazio do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Novo Banco de Dados** clicando com o botão direito do mouse na pasta **Bancos de Dados** de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Explorador de Objetos** e selecionando **Novo Banco de Dados**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome do banco de dados**|Digite o nome do novo banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Usar nome de usuário e senha específicos**|Selecione para fazer com que o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use as credenciais de segurança de uma conta de usuário especificada. As credenciais especificadas são usadas para processamento, consultas ROLAP, associações fora de linha, cubos locais, modelos de mineração, partições remotas, objetos vinculados e sincronização do destino para a origem. No entanto, para instruções OPENQUERY DMX, as credenciais do usuário atual são usadas.|  
|**Nome de usuário**|Digite o domínio e o nome da conta do usuário a serem usados pelo banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecionado. Use o seguinte formato:<br /><br /> *\<Nome de domínio >* ** \\ ** * \<nome da conta de usuário >*<br /><br /> Observação: essa opção será habilitada apenas se **Usar um nome de usuário e senha específicos** estiver selecionado.|  
|**Senha**|Digite a senha da conta de usuário especificada em **Nome de usuário**.|  
|**Usar a conta de serviço**|Selecione para fazer com que o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use as credenciais de segurança associadas ao serviço do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que gerencia o banco de dados. As credenciais da conta de serviço são usadas para processamento, consultas ROLAP, partições remotas, objetos vinculados e sincronização do destino para a origem. Para instruções OPENQUERY DMX, cubos locais e modelos de mineração as credenciais do usuário atual são usadas. Essa opção não tem suporte para associações fora de linha.|  
|**Usar as credenciais do usuário atual**|Selecione para fazer com que o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use as credenciais de segurança do usuário atual para associações fora de linha, instruções OPENQUERY DMX, cubos locais e modelos de mineração. A opção não tem suporte para processamento, consultas ROLAP, partições remotas, objetos vinculados e sincronização do destino para a origem.|  
|**Default**|Selecione para usar as credenciais da conta do usuário padrão do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Essa opção usa a configuração padrão do banco de dados para objetos de processamento, servidores de sincronização e execução de instruções de mineração de dados do **Open Query** . Para obter mais informações sobre como especificar as configurações padrão no nível do banco de dados, consulte [Definir propriedades do Banco de Dados Multidimensional &#40;Analysis Services&#41;](multidimensional-models/set-multidimensional-database-properties-analysis-services.md).<br /><br /> Por padrão o `DataSourceImpersonationInfo` banco de dados estiver definida como **usar a conta de serviço**. Independentemente do valor da propriedade `DataSourceImpersonationInfo`, as credenciais do usuário atual são usadas para associações fora de linha, consultas ROLAP, cubos locais e modelos de mineração de dados.|  
|**Descrição**|Digite a descrição do novo banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Bancos de dados modelo multidimensionais &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
