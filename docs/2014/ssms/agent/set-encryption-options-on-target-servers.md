---
title: Definir opções de criptografia em servidores de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 62267528b320f13c9dd35adc43761bf9a3f66f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011042"
---
# <a name="set-encryption-options-on-target-servers"></a>Definir opções de criptografia em servidores de destino
  Se você não puder usar um certificado para comunicações criptografadas em SSL (Secure Sockets Layer) entre os servidores mestres e parte ou todos os servidores de destino, mas quiser criptografar o canal entre eles, configure o servidor de destino para que use o nível de segurança necessário.  
  
 Para configurar o nível apropriado de segurança necessário para um canal de comunicação servidor mestre/servidor de destino específico, defina a subchave do Registro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*instance_name*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** no servidor de destino como um dos valores a seguir. O valor de \<*instance_name*> é **MSSQL.***n*. Por exemplo, **MSSQL.1** ou **MSSQL.3**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|Desabilita a criptografia entre este servidor de destino e o servidor mestre. Escolha esta opção apenas quando o canal entre o servidor de destino e servidor mestre estiver protegido por outros meios.|  
|**1**|Habilita criptografia apenas entre este servidor de destino e o servidor mestre, mas nenhuma validação de certificado é necessária.|  
|**2**|Habilita criptografia SSL completa e validação de certificado entre este servidor de destino e o servidor mestre. Esta é a configuração padrão. A menos que haja um motivo específico para escolher um valor diferente, nós recomendamos não alterá-la.|  
  
 Se **1** ou **2** for especificado, SSL deverá estar habilitado em ambos os servidores, mestre e de destino. Se **2** for especificado, também será necessário haver um certificado apropriadamente assinado no servidor mestre.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
  