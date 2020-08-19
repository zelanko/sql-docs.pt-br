---
description: Considerações sobre segurança XML
title: Considerações de segurança de XML | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 76ec899a26485a81a5ec81006d0dbd4c838738dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452488"
---
# <a name="xml-security-considerations"></a>Considerações sobre segurança XML
Os métodos Save e Open do ADO no objeto Recordset não são considerados operações seguras para serem executadas no Internet Explorer. Portanto, se esses métodos forem usados em um código de script que está sendo executado em um aplicativo ou controle hospedado em um navegador, a configuração de segurança do navegador terá um efeito sobre seu comportamento.  
  
 O Internet Explorer 5 fornece restrições de segurança para essas operações por padrão nas zonas da Internet. Nessa configuração, o conjunto de registros não pode fazer qualquer acesso ao sistema de arquivos local no cliente ou acessar quaisquer fontes de dados fora do domínio do servidor do qual a página foi baixada. Especificamente, ao executar dentro do host do navegador, um conjunto de registros poderá ser salvo novamente em um arquivo somente se ele estiver no mesmo servidor do qual a página foi baixada. Da mesma forma, você pode abrir um conjunto de registros carregando-o de um arquivo somente se esse arquivo estiver no mesmo servidor do qual a página foi baixada.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
