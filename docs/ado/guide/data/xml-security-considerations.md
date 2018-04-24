---
title: Considerações de segurança XML | Microsoft Docs
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
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbfee8717021fbc1eb621591987ee63ab54362e6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="xml-security-considerations"></a>Considerações de segurança XML
O ADO salvar e abrir métodos no objeto de conjunto de registros não são considerados seguras operações sejam executadas no Internet Explorer. Assim, se esses métodos são usados em um código de script que está em execução em um aplicativo ou um controle que é hospedado em um navegador, a configuração de segurança do navegador terá um efeito sobre seu comportamento.  
  
 O Internet Explorer 5 fornece restrições de segurança para essas operações por padrão nas zonas da Internet. Sob essa configuração, o conjunto de registros não é possível fazer qualquer acesso ao sistema de arquivos local no cliente ou acessar fontes de dados fora do domínio do servidor do qual a página foi baixada. Especificamente, quando é executado dentro do host do navegador, um conjunto de registros pode ser salvos para um arquivo apenas se estiver no mesmo servidor do qual a página foi baixada. Da mesma forma, você pode abrir um conjunto de registros por carregá-lo de um arquivo somente se esse arquivo está no mesmo servidor do qual a página foi baixada.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
