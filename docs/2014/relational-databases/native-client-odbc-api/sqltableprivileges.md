---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51492e55fd3c34c099a5f53187d1b2a9875ce7e3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349011"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
  **SQLTablePrivileges** pode ser executado em um cursor estático. Uma tentativa de executar **SQLTablePrivileges** em um cursor atualizável (controlado por conjunto de chaves ou dinâmico) retorna SQL_SUCCESS_WITH_INFO, indicando o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte a informações de relatórios para tabelas em servidores vinculados, aceitando um nome de duas partes para o *CatalogName* parâmetro: *Linked_server_name*.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLTablePrivileges] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
