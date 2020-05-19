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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f110447fbb0f00c037361b00945b228449caf4f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747719"
---
# <a name="registering-a-custom-business-object"></a>Registrar um objeto de negócios personalizado
Para iniciar com êxito um objeto comercial personalizado (. dll ou. exe) por meio do servidor Web, o ProgID do objeto comercial deve ser inserido no registro, conforme explicado neste procedimento. Esse recurso RDS protege a segurança do seu servidor Web executando somente executáveis aprovados.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Para o MDAC 2,0 e posterior e o DAC do Windows, o objeto comercial padrão, [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), não é registrado por padrão durante a instalação do DAC do MDAC/Windows. No entanto, se **RDSServer. datafactory** tiver sido registrado como seguro para execução no computador antes da instalação, a entrada do registro será mantida para a nova instalação.  
  
### <a name="to-register-a-custom-business-object"></a>Para registrar um objeto comercial personalizado:  
  
1.  Clique em **Iniciar** e em **executar**.  
  
2.  Digite **regedit** e clique em **OK**.  
  
3.  No editor do registro, navegue até a chave do registro **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch** .  
  
4.  Selecione a chave **ADCLaunch** e, em seguida, no menu **Editar**, aponte para **novo** e clique em **chave**.  
  
5.  Digite o ProgID do seu objeto comercial personalizado e clique em **Enter**. Deixe a entrada **valor** em branco.


