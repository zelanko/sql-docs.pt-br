---
title: Considerações sobre segurança XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e80a0bbb70a626ff01043592896ecfbe3c21f189
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802875"
---
# <a name="xml-security-considerations"></a>Considerações sobre segurança XML
O ADO salvar e abrir métodos no objeto de conjunto de registros não são considerados operações seguras para ser executado no Internet Explorer. Portanto, se esses métodos são usados em um código de script que está em execução em um aplicativo ou controle que está hospedado em um navegador, a configuração de segurança do navegador terá um efeito sobre seu comportamento.  
  
 O Internet Explorer 5 fornece restrições de segurança para essas operações, por padrão nas zonas da Internet. Em que a configuração, o conjunto de registros não é possível fazer qualquer acesso ao sistema de arquivos local no cliente ou acessar quaisquer fontes de dados fora do domínio do servidor do qual a página tiver sido baixada. Especificamente, quando em execução dentro do host do navegador, um conjunto de registros pode ser salvos para um arquivo somente se ele está no mesmo servidor do qual a página foi baixada. Da mesma forma, você pode abrir um conjunto de registros carregá-los a partir de um arquivo somente se esse arquivo estiver no mesmo servidor do qual a página foi baixada.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
