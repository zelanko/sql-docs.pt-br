---
title: Códigos de retorno | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00082a5c6053d8b9f0319c26ae8d72302c14d218
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407620"
---
# <a name="return-codes"></a>Códigos de retorno
  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno de OLE DB, consulte [códigos de retorno (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor OLE DB do Native Client Retorna S_OK, a função teve êxito.  
  
 Quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor OLE DB do Native Client não retorna S_OK, as macros HRESULT de OLE/COM falha e IS_ERROR podem determinar o êxito ou falha de uma função geral.  
  
 Se FAILED ou IS_ERROR retornar TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client terá certeza de que houve falha na execução da função de membro. Quando FAILED ou IS_ERROR retornar FALSE e o HRESULT não é igual a S_OK, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client terá certeza de que a função foi bem-sucedida de alguma forma. O consumidor pode recuperar informações detalhadas sobre essa "êxito com informações" retorna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor OLE DB do Native Client. Além disso, no caso em que uma função falhar claramente (a macro FAILED retornar TRUE), informações de erro estendidas serão proveniente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor OLE DB do Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os consumidores de provedor Native Client OLE DB comumente encontram o retorno HRESULT DB_S_ERRORSOCCURRED "êxito com informações". Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Talvez nenhuma informação de erro esteja disponível para o consumidor além daquela retornada em parâmetros de valor de status; assim, os consumidores devem implementar a lógica de aplicativo para recuperar valores de status quando eles estiverem disponíveis.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor OLE DB do Native Client não retornam o código de êxito S_FALSE. Todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor OLE DB do Native Client sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](errors.md)  
  
  
