---
title: Códigos de retorno | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 625d56a38d88b3cccbea1c75ad88917af1a6f6dd
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368088"
---
# <a name="return-codes"></a>Códigos de retorno
  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno do OLE DB, confira [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor OLE DB do Native Client Retorna S_OK, a função teve êxito.  
  
 Quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor OLE DB do Native Client não retorna S_OK, as macros HRESULT de OLE/COM falha e IS_ERROR podem determinar o êxito ou falha de uma função geral.  
  
 Se FAILED ou IS_ERROR retornar TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client terá certeza de que houve falha na execução da função de membro. Quando FAILED ou IS_ERROR retornar FALSE e o HRESULT não é igual a S_OK, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client terá certeza de que a função foi bem-sucedida de alguma forma. O consumidor pode recuperar informações detalhadas sobre essa "êxito com informações" retorna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor OLE DB do Native Client. Além disso, no caso em que uma função falhar claramente (a macro FAILED retornar TRUE), informações de erro estendidas serão proveniente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor OLE DB do Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os consumidores de provedor Native Client OLE DB comumente encontram o retorno HRESULT DB_S_ERRORSOCCURRED "êxito com informações". Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Talvez nenhuma informação de erro esteja disponível para o consumidor além daquela retornada em parâmetros de valor de status; assim, os consumidores devem implementar a lógica de aplicativo para recuperar valores de status quando eles estiverem disponíveis.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor OLE DB do Native Client não retornam o código de êxito S_FALSE. Todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor OLE DB do Native Client sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](errors.md)  
  
  
