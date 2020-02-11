---
title: Propriedades de distribuição | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 283fd67d14d57c3d1d5d60dd9d8de2a159ca6d5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721366"
---
# <a name="distribution-database"></a>Banco de dados de distribuição
  O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional.  
  
 Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos. Você pode especificar um banco de dados de distribuição para o Distribuidor usando o Assistente para Configurar a Distribuição. Se necessário, especifique bancos de dados de distribuição adicionais na caixa de diálogo **Propriedades do Distribuidor** .  
  
## <a name="options"></a>Opções  
 **Nome do banco de dados de distribuição**  
 Insira um nome para o banco de dados de distribuição. O nome padrão para o banco de dados de distribuição é “distribuição”. Se você especificar um nome, o nome pode ter, no máximo, 128 caracteres, deve ser exclusivo dentro de uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância do e deve estar em conformidade com as regras para identificadores. Para obter mais informações, consulte [Database Identifiers](../databases/database-identifiers.md).  
  
 **Pasta do arquivo** e da pasta do banco de dados de distribuição **para o arquivo de log do banco de dados de distribuição**  
 Insira o caminho para o banco de dados de distribuição e arquivos de log. Os caminhos devem se referir aos discos locais do Distribuidor e começar com uma letra de unidade e dois pontos (por exemplo, C:). Letras de unidades e caminhos de rede mapeados não são válidos.  
  
> [!NOTE]  
>  Você pode diminuir o tempo de gravação das transações e aprimorar o desempenho da replicação colocando o log do banco de dados de distribuição em uma unidade de disco separada do banco de dados de distribuição.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](configure-distribution.md)   
 [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)  
  
  
