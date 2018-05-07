---
title: Propriedades de segurança | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8c587bbe18f99779889960a94f68ad43bde59b76
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="security-properties"></a>Propriedades de segurança
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de segurança listadas na tabela a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## <a name="properties"></a>Propriedades  
 **RequireClientAuthentication**  
 Uma propriedade booliana que indica se autenticação de cliente é necessária.  
  
 O valor padrão para essa propriedade é True, o que indica que autenticação de cliente é necessária.  
  
 **SecurityPackageList**  
 Uma propriedade de cadeia de caracteres que contém uma lista separada por vírgulas de pacotes SSPI usada pelo servidor para autenticação de cliente.  
  
 **DisableClientImpersonation**  
 Uma propriedade booliana que indica se a representação do cliente (por exemplo, de procedimentos armazenados) está desabilitada.  
  
 O valor padrão dessa propriedade é False, o que indica que representação do cliente está habilitada.  
  
 **BuiltinAdminsAreServerAdmins**  
 Uma propriedade booliana que indica se membros do grupo de administradores de máquina local são administradores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **ServiceAccountIsServerAdmin**  
 Uma propriedade booliana que indica se a conta de serviço é um administrador do servidor.  
  
 O valor padrão dessa propriedade é True, o que indica que a conta de serviço é um administrador do servidor.  
  
 **ErrorMessageMode**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataProtection\ RequiredProtectionLevel**  
 Uma propriedade de inteiro de 32 bits assinada que define o nível de proteção exigido para todas as requisições do cliente. Essa propriedade tem um dos valores listados na tabela a seguir:  
  
|Value|Descrição|  
|-----------|-----------------|  
|*0*|Nenhum, texto não criptografado permitido.|  
|*1*|(Padrão) Criptografia necessária, sem log de texto não criptografado.|  
|*2*|Solicitações de textos não criptografados são permitidas, mas apenas com assinaturas (proteção mais baixa do que criptografia).|  
  
 **AdministrativeDataProtection\ RequiredProtectionLevel**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
