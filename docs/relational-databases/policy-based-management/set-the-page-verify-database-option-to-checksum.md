---
title: Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM | Microsoft Docs
description: Verifique se a opção PAGE_VERIFY é CHECKSUM, que controla se o Mecanismo de Banco de Dados do SQL Server calcula uma soma de verificação para ajudar a fornecer a integridade do arquivo de dados.
ms.custom: ''
ms.date: 08/19/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646506"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>Definir a opção do banco de dados PAGE_VERIFY como CHECKSUM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica se a opção do banco de dados PAGE_VERIFY está definida como CHECKSUM. Quando CHECKSUM é habilitado para a opção do banco de dados PAGE_VERIFY, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula uma soma de verificação nos conteúdos da página inteira e armazena o valor no cabeçalho da página, quando uma página é gravada em disco. Quando a página é lida pelo disco, a soma de verificação é recalculada e comparada ao valor da soma de verificação armazenado no cabeçalho da página. Isso ajuda a fornecer um alto nível de integridade de arquivo de dados.  Se você usar a opção PAGE_VERIFY CHECKSUM para um banco de dados, quando o SQL Server detectar que uma página foi alterada após ser gravada em disco, ele reportará uma [mensagem de erro 824](../errors-events/mssqlserver-824-database-engine-error.md) depois de ler a página de volta do disco. 
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM. O uso da opção do banco de dados PAGE_VERIFY CHECKSUM pode fornecer a detecção mais robusta de problemas de consistência de banco de dados causados pelo caminho de E/S do sistema.
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
