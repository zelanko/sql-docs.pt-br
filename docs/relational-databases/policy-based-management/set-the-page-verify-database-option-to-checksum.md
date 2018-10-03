---
title: Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20f97815b85b7cf88baad386bda43596c5ac81a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784624"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>Definir a opção do banco de dados PAGE_VERIFY como CHECKSUM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se a opção do banco de dados PAGE_VERIFY está definida como CHECKSUM. Quando CHECKSUM é habilitado para a opção do banco de dados PAGE_VERIFY, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula uma soma de verificação nos conteúdos da página inteira e armazena o valor no cabeçalho da página, quando uma página é gravada em disco. Quando a página é lida pelo disco, a soma de verificação é recalculada e comparada ao valor da soma de verificação armazenado no cabeçalho da página. Isso ajuda a fornecer um alto nível de integridade de arquivo de dados.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
