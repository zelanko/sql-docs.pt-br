---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa0e9e2df1e8ba3f44b10e662d25e536ac7962f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923355"
---
# <a name="xml-security-considerations"></a>Considerações sobre segurança XML
Os métodos Save e Open do ADO no objeto Recordset não são considerados operações seguras para serem executadas no Internet Explorer. Portanto, se esses métodos forem usados em um código de script que está sendo executado em um aplicativo ou controle hospedado em um navegador, a configuração de segurança do navegador terá um efeito sobre seu comportamento.  
  
 O Internet Explorer 5 fornece restrições de segurança para essas operações por padrão nas zonas da Internet. Nessa configuração, o conjunto de registros não pode fazer qualquer acesso ao sistema de arquivos local no cliente ou acessar quaisquer fontes de dados fora do domínio do servidor do qual a página foi baixada. Especificamente, ao executar dentro do host do navegador, um conjunto de registros poderá ser salvo novamente em um arquivo somente se ele estiver no mesmo servidor do qual a página foi baixada. Da mesma forma, você pode abrir um conjunto de registros carregando-o de um arquivo somente se esse arquivo estiver no mesmo servidor do qual a página foi baixada.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
