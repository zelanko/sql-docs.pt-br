---
title: Registrando um objeto comercial personalizado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f998463e0f8190aa040b801d2fd29c732bb31dce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922363"
---
# <a name="registering-a-custom-business-object"></a>Registrar um objeto de negócios personalizado
Para iniciar com êxito um objeto comercial personalizado (. dll ou .exe) por meio do servidor Web, o ProgID do objeto comercial deve ser inserido para o registro conforme explicado neste procedimento. Esse recurso RDS protege a segurança do seu servidor Web executando somente os executáveis sancionados.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Para Windows DAC, o objeto de negócios padrão e o MDAC 2.0 e posterior [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), não é registrado por padrão durante a instalação de MDAC/Windows DAC. No entanto, se **RDSServer.DataFactory** foi registrado como seguros para execução no computador antes da instalação, a entrada do registro é mantida para a nova instalação.  
  
### <a name="to-register-a-custom-business-object"></a>Para registrar um objeto comercial personalizado:  
  
1.  Clique em **inicie** e, em seguida, clique em **executar**.  
  
2.  Tipo de **RegEdit** e clique em **Okey**.  
  
3.  No Editor do registro, navegue até a **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** chave do registro.  
  
4.  Selecione o **ADCLaunch** chave e, em seguida, o **editar**, aponte para **New** e clique em **chave**.  
  
5.  Digite o ProgID do seu objeto de negócios personalizada e clique em **Enter**. Deixe o **valor** entrada em branco.


