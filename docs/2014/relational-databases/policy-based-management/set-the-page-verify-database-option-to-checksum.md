---
title: Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 13296a976722390668b8ca6d901cf0dd080e5cc3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066655"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>Definir a opção do banco de dados PAGE_VERIFY como CHECKSUM
  Esta regra verifica se a opção do banco de dados PAGE_VERIFY está definida como CHECKSUM. Quando CHECKSUM é habilitado para a opção do banco de dados PAGE_VERIFY, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula uma soma de verificação nos conteúdos da página inteira e armazena o valor no cabeçalho da página, quando uma página é gravada em disco. Quando a página é lida pelo disco, a soma de verificação é recalculada e comparada ao valor da soma de verificação armazenado no cabeçalho da página. Isso ajuda a fornecer um alto nível de integridade de arquivo de dados.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
