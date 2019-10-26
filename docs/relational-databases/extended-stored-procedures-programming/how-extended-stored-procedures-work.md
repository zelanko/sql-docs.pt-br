---
title: Como funcionam os procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 42aad667b6081e79b4b7897d4dd1f354a6148e8b
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72904046"
---
# <a name="how-extended-stored-procedures-work"></a>Como funcionam os procedimentos armazenados estendidos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 O processo pelo qual um procedimento armazenado estendido funciona é o seguinte:  
  
1.  Quando um cliente executa um procedimento armazenado estendido, a solicitação é transmitida no protocolo TDS ou no formato SOAP (Simple Object Access Protocol) do aplicativo cliente para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa a DLL associada com o procedimento armazenado estendido e carrega a DLL, se ela já não estiver carregada.  
  
3.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama o procedimento armazenado estendido solicitado (implementado como uma função dentro da DLL).  
  
4.  O procedimento armazenado estendido passa conjuntos de resultados e parâmetros de retorno de volta ao servidor por meio da API de procedimento armazenado estendido.  

