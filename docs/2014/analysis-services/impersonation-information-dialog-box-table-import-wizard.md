---
title: Caixa de diálogo de informações sobre representação (Assistente de importação de tabela) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d271bbfdf31a24304961d71e4501ea7ae4579440
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047557"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>Caixa de diálogo de informações de representação (Assistente de Importação de Tabela)
  Use a página **Informações sobre Representação** para especificar as credenciais que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará para se conectar à fonte de dados. Para obter mais informações sobre como a representação de credenciais, consulte [Impersonation &#40;SSAS Tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
## <a name="options"></a>Opções  
 **Senha e nome de usuário específicos do Windows**  
 Selecione esta opção para fazer com que o modelo tabular use as credenciais de segurança de uma conta de usuário do Windows especificada.  
  
 **Nome de usuário**  
 Digite o domínio e o nome da conta de usuário a serem usados. Use o seguinte formato:  
  
 *\<Nome de domínio >* **\\**  *\<nome da conta de usuário >*  
  
 Essa opção estará habilitada apenas se a opção **Usar um nome e uma senha específicos** estiver selecionada.  
  
 **Senha**  
 Digite a senha da conta de usuário a ser usada pelo objeto do modelo tabular.  
  
 Essa opção estará habilitada apenas se a opção **Usar um nome e uma senha específicos** estiver selecionada.  
  
 **Conta de serviço**  
 Selecione esta opção para usar as credenciais de segurança associadas ao serviço [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que gerencia o modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Representação &#40;Tabular do SSAS&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  
