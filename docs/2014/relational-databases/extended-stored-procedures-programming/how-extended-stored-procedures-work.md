---
title: Como funcionam os procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9b52e8fd5cda7d0b05ebbddbb422f74bd81b1993
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62512988"
---
# <a name="how-extended-stored-procedures-work"></a>Como funcionam os procedimentos armazenados estendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 O processo pelo qual um procedimento armazenado estendido funciona é o seguinte:  
  
1.  Quando um cliente executa um procedimento armazenado estendido, a solicitação é transmitida no protocolo TDS ou no formato SOAP (Simple Object Access Protocol) do aplicativo cliente para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o.  
  
2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa a DLL associada com o procedimento armazenado estendido e carrega a DLL, se ela já não estiver carregada.  
  
3.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama o procedimento armazenado estendido solicitado (implementado como uma função dentro da DLL).  
  
4.  O procedimento armazenado estendido passa conjuntos de resultados e parâmetros de retorno de volta ao servidor por meio da API de procedimento armazenado estendido.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação do procedimento armazenado estendido do mecanismo do banco de dados](../database-engine-extended-stored-procedure-programming.md)  
  
  
