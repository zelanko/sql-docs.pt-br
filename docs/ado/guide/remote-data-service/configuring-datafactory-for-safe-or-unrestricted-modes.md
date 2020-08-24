---
description: Configurar o DataFactory para modos seguros ou irrestritos
title: Configurando o datafactory para modos seguros ou irrestritos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: rothja
ms.author: jroth
ms.openlocfilehash: ffd9c1b82225a131722cdaf384c4bd5662b5322f
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758386"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configurar o DataFactory para modos seguros ou irrestritos
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por padrão, o ADO é instalado com uma configuração "Safe" de [RDSServer. datafactory](../../reference/rds-api/datafactory-object-rdsserver.md) . O modo de segurança para componentes do servidor RDS significa que o seguinte é verdadeiro:  
  
1.  O manipulador é necessário com o RDSServer. datafactory (isso é obrigatório por uma configuração de chave do registro).  
  
2.  O manipulador padrão, msdfmap. Handler, é registrado, está presente na lista de manipuladores seguros e marcado como o manipulador padrão.  
  
3.  Msdfmap.ini arquivo é instalado no diretório do Windows. Você deve configurar esse arquivo de acordo com suas necessidades, antes de usar o RDS no modo de três camadas.  
  
 Opcionalmente, você pode configurar uma instalação de **DataFactory** irrestrita. **DataFactory** pode ser usado diretamente sem o manipulador personalizado. Os usuários ainda podem usar um manipulador personalizado modificando as cadeias de conexão, mas isso não é necessário. Para obter mais informações sobre as implicações de usar o objeto **RDSServer. datafactory** , consulte [Securing RDS Applications](./securing-rds-applications.md).  
  
 O arquivo de registro handsafe. reg foi fornecido para configurar as entradas do registro do manipulador para uma configuração segura. Para executar em modo de segurança, execute handsafe. reg.  
  
 Depois de executar o handsafe. reg, você deve parar e reiniciar o serviço de publicação de World Wide Web no servidor Web digitando os seguintes comandos em uma janela de prompt de comando: "NET STOP W3SVC" e "NET START W3SVC".  
  
## <a name="see-also"></a>Consulte Também  
 [Personalização de datafactory](./datafactory-customization.md)   
 [Conceitos básicos do RDS](./rds-fundamentals.md)