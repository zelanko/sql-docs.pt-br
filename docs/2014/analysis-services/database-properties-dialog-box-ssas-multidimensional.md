---
title: Caixa de diálogo de propriedades (SSAS - Multidimensional) do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a18669d646dcf6e46f609faeb0861e5fa9732850
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732539"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>Caixa de diálogo Propriedades do Banco de Dados (SSAS – Multidimensional)
  Use a caixa de diálogo **Propriedades do Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as propriedades de uma base de dados em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Você pode exibir a caixa de diálogo **Propriedades do Banco de Dados** clicando com o botão direito do mouse em um banco de dados no Pesquisador de Objetos e selecionando **Propriedades**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Digite para alterar o nome do banco de dados.|  
|**ID**|Exibe o identificador do banco de dados.|  
|**Descrição**|Digite para alterar a descrição do banco de dados.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação do banco de dados.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados do banco de dados.|  
|**Última atualização**|Exibe a data e a hora da última atualização dos dados do banco de dados.|  
|**Informações de representação de fonte de dados**|Selecione as informações de representação usadas pelo banco de dados ao conectar-se e interagir com as fontes de dados contidas pelo banco de dados. Os valores válidos incluem os seguintes:<br /><br /> **ImpersonateAccount** (use uma senha e um nome de usuário específicos do Windows).<br /><br /> **ImpersonateService** (use a conta de serviço).<br /><br /> **ImpersonateCurrentUser** (use as credenciais do usuário atual).<br /><br /> **Default** (use a conta de serviço para operações MOLAP e o usuário atual para mineração de dados).<br /><br /> Embora você possa definir as configurações de representação de fonte de dados no nível do banco de dados, fazer isso afetará apenas as fontes de dados que especificarem **Herdar** para suas configurações de representação. As configurações de representação especificadas diretamente na fonte de dados sempre substituirão as configurações especificadas no nível do banco de dados.<br /><br /> Ao escolher uma opção de representação, considere os tipos de operações que precisarão de suporte. Algumas operações, como processar, não podem ser executadas por|  
|**Último processamento**|Exibe a data e a hora do último processamento do banco de dados.|  
|**Tamanho estimado**|Exibe o tamanho estimado do banco de dados.|  
|**Local de armazenamento**|Especifica o local do banco de dados. Se o banco de dados for localizado no diretório de Dados padrão, esse valor será vazio.|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
