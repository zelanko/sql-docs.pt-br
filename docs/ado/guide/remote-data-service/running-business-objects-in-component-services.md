---
title: Executando objetos de negócios em serviços de componente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f64909f4f7db1f765d233878631eb90a4760531e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704207"
---
# <a name="running-business-objects-in-component-services"></a>Executar objetos de negócios nos serviços de componentes
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Objetos de negócios podem ser arquivos executáveis (.exe) ou bibliotecas de vínculo dinâmico (. dll). A configuração que você usa para executar o objeto comercial depende se o objeto é um arquivo. dll ou .exe:  
  
-   Objetos de negócios criados como .exe arquivos podem ser chamados por meio do DCOM. Se esses objetos comerciais são usados por meio de serviços de informações da Internet (IIS), isso quer dizer que eles estão sujeitos a adicionais de marshaling de dados, o que reduzirá o desempenho do cliente.  
  
-   Objetos de negócios criados como arquivos. dll podem ser usados por meio do IIS e, portanto, também pelo HTTP. Eles também podem ser usados ao DCOM somente por meio de serviços de componentes ou por meio de Microsoft Transaction Server, se você estiver usando o Windows NT. O objeto de negócios DLLs precisará ser registrado no computador do servidor IIS para acessá-los por meio do IIS. Para obter informações sobre como configurar uma DLL para ser executado no DCOM, consulte a seção [habilitando um DLL para ser executado em DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Quando os objetos de negócios na camada intermediária são implementados como componentes de serviços de componentes usando **GetObjectContext**, **SetComplete**, e **SetAbort**, os negócios objetos podem usar serviços de componentes (ou MTS, se você estiver usando o Windows NT) objetos de contexto para manter seu estado em várias chamadas de cliente. Esse cenário é possível com DCOM, que geralmente é implementado entre clientes confiáveis e servidores em uma intranet. Nesse caso, o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto e [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método no lado do cliente são substituídos pelo objeto de contexto de transação e **CreateInstance** método, que são fornecidos pelo **ITransactionContext** de interface e implementados pelos serviços de componente.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


