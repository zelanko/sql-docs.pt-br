---
title: "Propriedades de seguran&#231;a  | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "segurança [Analysis Services], propriedade"
  - "propriedade SecurityPackageList"
  - "propriedade BuiltinAdminsAreServerAdmins"
  - "propriedade DisableClientImpersonation"
  - "propriedade ErrorMessageMode"
  - "propriedade RequiredProtectionLevel"
  - "propriedade ServiceAccountIsServerAdmin"
  - "propriedade RequireClientAuthentication"
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# Propriedades de seguran&#231;a 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de segurança listadas na tabela a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## Propriedades  
 **RequireClientAuthentication**  
 Uma propriedade booliana que indica se autenticação de cliente é necessária.  
  
 O valor padrão para essa propriedade é True, o que indica que autenticação de cliente é necessária.  
  
 **SecurityPackageList**  
 Uma propriedade de cadeia de caracteres que contém uma lista separada por vírgulas de pacotes SSPI usada pelo servidor para autenticação de cliente.  
  
 **DisableClientImpersonation**  
 Uma propriedade booliana que indica se a representação do cliente (por exemplo, de procedimentos armazenados) está desabilitada.  
  
 O valor padrão dessa propriedade é False, o que indica que representação do cliente está habilitada.  
  
 **BuiltinAdminsAreServerAdmins**  
 Uma propriedade booliana que indica se membros do grupo de administradores de máquina local são administradores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
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
  
## Consulte também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  