---
title: MSSQLSERVER_33085 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 33085 (Database Engine error)
ms.assetid: c27b8d1d-668a-4ba8-8b61-25a5ebbc5485
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a0a4c315a40a70084e1f97f5b3c52081356d4aa0
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver33085"></a>MSSQLSERVER_33085
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|33085|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROVE_METHOD_CANNOT_FOUND|  
|Texto da mensagem|Não é possível encontrar um ou mais métodos na biblioteca de provedor criptográfica '%. * ls.'|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde usar o provedor criptográfico listado na mensagem de erro. O provedor criptográfico não deu suporte a um método exigido. O estado do erro indica qual método não foi encontrado.  
  
|Estado|Description|  
|---------|---------------|  
|1|SqlCryptInitializeProvider|  
|2|SqlCryptFreeProvider|  
|3|SqlCryptOpenSession|  
|4|SqlCryptCloseSession|  
|5|SqlCryptGetProviderInfo|  
|6|SqlCryptGetNextAlgorithmId|  
|7|SqlCryptGetAlgorithmInfo|  
|8|SqlCryptCreateKey|  
|9|SqlCryptDropKey|  
|10|SqlCryptGetNextKeyId|  
|11|SqlCryptGetKeyInfoByKeyId|  
|12|SqlCryptGetKeyInfoByThumb|  
|13|SqlCryptGetKeyInfoByName|  
|14|SqlCryptExportKey|  
|15|SqlCryptImportKey|  
|16|SqlCryptEncrypt|  
|17|SqlCryptDecrypt|  
  
## <a name="user-action"></a>Ação do usuário  
Contate o provedor criptográfico para obter mais informações.  
  

