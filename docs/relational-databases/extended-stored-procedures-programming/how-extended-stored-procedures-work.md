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
manager: craigg
ms.openlocfilehash: ab0864e8eb320c63bd757d4c6edab384c6c821b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742232"
---
# <a name="how-extended-stored-procedures-work"></a>Como funcionam os procedimentos armazenados estendidos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 O processo pelo qual um procedimento armazenado estendido funciona é o seguinte:  
  
1.  Quando um cliente executa um procedimento armazenado estendido, a solicitação é transmitida em formato de protocolo de acesso a objeto simples (SOAP) do aplicativo cliente para ou de fluxo de dados de tabela (TDS) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa a DLL associada com o procedimento armazenado estendido e carrega a DLL, se ela já não estiver carregada.  
  
3.  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama o procedimento armazenado estendido solicitado (implementado como uma função dentro da DLL).  
  
4.  O procedimento armazenado estendido passa conjuntos de resultados e parâmetros de retorno de volta ao servidor por meio da API de procedimento armazenado estendido.  
