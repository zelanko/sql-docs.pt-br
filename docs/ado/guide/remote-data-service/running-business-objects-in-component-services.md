---
description: Executar objetos de negócios nos serviços de componentes
title: Executando objetos comerciais em serviços de componentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: rothja
ms.author: jroth
ms.openlocfilehash: 4343d8e1bd04d7e8044fa7f3f1b5de6184466d3f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977717"
---
# <a name="running-business-objects-in-component-services"></a>Executar objetos de negócios nos serviços de componentes
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Os objetos comerciais podem ser arquivos executáveis (. exe) ou bibliotecas de vínculo dinâmico (. dll). A configuração usada para executar o objeto comercial depende de se o objeto é um arquivo. dll ou. exe:  
  
-   Os objetos comerciais criados como arquivos. exe podem ser chamados por meio do DCOM. Se esses objetos comerciais forem usados por meio do Serviços de Informações da Internet (IIS), eles estarão sujeitos a marshaling adicional de dados, o que reduzirá o desempenho do cliente.  
  
-   Os objetos comerciais criados como arquivos. dll podem ser usados por meio do IIS e, portanto, também por HTTP. Eles também podem ser usados sobre DCOM somente por meio de serviços de componentes, ou por meio do Microsoft Transaction Server, se você estiver usando o Windows NT. As DLLs de objeto comercial precisarão ser registradas no computador do servidor IIS para acessá-las por meio do IIS. Para obter informações sobre como configurar uma DLL para ser executada no DCOM, consulte a seção [habilitando uma dll para ser executada no DCOM](./enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Quando os objetos comerciais na camada intermediária são implementados como componentes de serviços de componentes usando **getObjectContext**, **SetComplete**e **SetAbort**, os objetos de negócios podem usar os serviços de componentes (ou MTS, se você estiver usando o Windows NT) objetos de contexto para manter seu estado entre várias chamadas de cliente. Esse cenário é possível com o DCOM, que normalmente é implementado entre clientes e servidores confiáveis em uma intranet. Nesse caso, o [RDS. O objeto DataSpace](../../reference/rds-api/dataspace-object-rds.md) e o método [CreateObject](../../reference/rds-api/createobject-method-rds.md) no lado do cliente são substituídos pelo método **CreateInstance** e pelo objeto de contexto da transação, que são fornecidos pela interface **ITransactionContext** e implementados pelos serviços de componentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](./rds-fundamentals.md)