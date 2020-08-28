---
description: Configurar o DataFactory para modos seguros ou irrestritos
title: Configurando o datafactory para modos seguros ou irrestritos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: rothja
ms.author: jroth
ms.openlocfilehash: ab1236205813d1fa3aee0a039703afb10661169c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978357"
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