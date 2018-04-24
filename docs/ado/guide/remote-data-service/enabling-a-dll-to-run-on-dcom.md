---
title: Habilitando uma DLL para ser executado em DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f21cdd1b8a60a978ad87923f2e5039554533146d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitando um DLL seja executada em DCOM
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 As etapas a seguir descrevem como habilitar um objeto de negócios. dll usar o Microsoft Internet informações de serviços (HTTP) por meio de serviços de componentes e DCOM.  
  
1.  Crie um novo pacote vazio no snap-in de MMC de serviços de componente.  
  
     Você usará o snap-in do MMC dos serviços de componentes para criar um pacote e adicionar a DLL para este pacote. Isso torna o arquivo. dll acessível por meio do DCOM, mas ele remove a acessibilidade por meio do IIS. (Se você verificar o registro para o arquivo. dll, o **Inproc** chave agora está vazia; definir o atributo de ativação, explicado posteriormente neste tópico, adiciona um valor na **Inproc** chave.)  
  
2.  Instale um objeto de negócios no pacote.  
  
     -ou-  
  
     Importar o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto no pacote.  
  
3.  Defina o atributo de ativação para o pacote de **no processo do criador** (aplicativo de biblioteca).  
  
     Para tornar o arquivo. dll acessível por meio do DCOM e IIS no mesmo computador, você deve definir o atributo de ativação do componente de snap-in MMC de serviços de componente. Depois de definir o atributo para **no processo do criador**, você observará que uma **Inproc** chave no registro do servidor foi adicionada que aponta para um componente de serviços substitutos. dll.  
  
 Para obter mais informações sobre serviços de componentes (ou Microsoft Transaction Service, se você estiver usando o Windows NT) e como executar essas etapas, visite o site do Microsoft Transaction Server.


