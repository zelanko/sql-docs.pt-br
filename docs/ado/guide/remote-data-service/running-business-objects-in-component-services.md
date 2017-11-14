---
title: "Executando objetos de negócios nos serviços de componentes | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a4c05f997a09e2a3368c47ce5038c17421867172
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="running-business-objects-in-component-services"></a>Executando objetos de negócios nos serviços de componentes
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Objetos de negócios podem ser arquivos executáveis (.exe) ou bibliotecas de vínculo dinâmico (. dll). A configuração que você usa para executar o objeto comercial depende se o objeto é um arquivo. dll ou .exe:  
  
-   Objetos de negócios criados como arquivos de .exe podem ser chamados por meio do DCOM. Se esses objetos de negócios são usados por meio de serviços de informações da Internet (IIS), eles são sujeitas a empacotamento adicionais de dados, o que reduzirá o desempenho do cliente.  
  
-   Objetos de negócios criados como arquivos. dll podem ser usados pelo IIS e, portanto, também por HTTP. Eles também podem ser usados ao DCOM somente por meio de serviços de componentes ou Microsoft Transaction Server, se você estiver usando o Windows NT. Objeto comercial DLLs precisa ser registrado no computador do servidor IIS para acessá-los por meio do IIS. Para obter informações sobre como configurar um DLL seja executada em DCOM, consulte a seção [habilitando uma DLL para ser executado em DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Quando os objetos de negócios na camada intermediária são implementados como componentes de serviços de componentes usando **GetObjectContext**, **SetComplete**, e **SetAbort**, a empresa objetos podem usar serviços de componentes (ou MTS, se você estiver usando o Windows NT) objetos de contexto para manter seu estado em várias chamadas de cliente. Este cenário é possível com DCOM, que costuma ser implementada entre clientes confiáveis e servidores em uma intranet. Nesse caso, o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto e [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método no lado do cliente são substituídos pelo objeto de contexto de transação e **CreateInstance** método, que são fornecidos pelo **ITransactionContext** interface e implementados pelos serviços de componente.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



