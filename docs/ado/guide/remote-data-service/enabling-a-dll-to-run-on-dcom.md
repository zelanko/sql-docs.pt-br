---
title: Habilitando um DLL para ser executado em DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccfb1189e0c4d9bb0b1684ac3fd47709f491cd48
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704561"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitar um DLL para ser executado no DCOM
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 As etapas a seguir descrevem como habilitar um objeto de negócios. dll usar o DCOM e serviços de informações de Internet (HTTP) do Microsoft por meio de serviços de componentes.  
  
1.  Crie um novo pacote vazio no snap-in de MMC de serviços de componente.  
  
     Você usará o snap-in MMC de serviços de componentes para criar um pacote e adicionar a DLL para esse pacote. Isso torna o arquivo. dll acessível por meio do DCOM, mas ele remove a acessibilidade por meio do IIS. (Se você fazer check-in do registro para o arquivo. dll, o **Inproc** chave agora está vazia; definindo o atributo de ativação, explicado mais adiante neste tópico, adiciona um valor na **Inproc** chave.)  
  
2.  Instale um objeto de negócios no pacote.  
  
     -ou-  
  
     Importar o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto no pacote.  
  
3.  Defina o atributo de ativação para o pacote **no processo do criador** (aplicativo de biblioteca).  
  
     Para disponibilizar o arquivo. dll por meio do DCOM e o IIS no mesmo computador, você deve definir o atributo de ativação do componente no snap-in de MMC de serviços de componente. Depois de definir o atributo como **no processo do criador**, você observará que uma **Inproc** chave no registro do servidor tiver sido adicionada, que aponta para um componente de serviços substitutos. dll.  
  
 Para obter mais informações sobre serviços de componentes (ou serviço de transação da Microsoft, se você estiver usando o Windows NT) e como executar essas etapas, visite o site do Microsoft Transaction Server.


