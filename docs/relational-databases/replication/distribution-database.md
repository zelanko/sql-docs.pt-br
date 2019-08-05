---
title: Propriedades de distribuição | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 8c07f5b46b1f09f54ce152eeaccabd695b0f32ed
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770682"
---
# <a name="distribution-database"></a>Banco de dados de distribuição
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  O banco de dados de distribuição armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional.  
  
 Em muitos casos, um único banco de dados de distribuição é suficiente. Porém, se vários Publicadores usarem um único Distribuidor, considere criar um banco de dados de distribuição para cada Publicador. Fazer isso assegura que os dados que fluem por cada banco de dados de distribuição são distintos. Você pode especificar um banco de dados de distribuição para o Distribuidor usando o Assistente para Configurar a Distribuição. Se necessário, especifique bancos de dados de distribuição adicionais na caixa de diálogo **Propriedades do Distribuidor** .  
  
## <a name="options"></a>Opções  
 **Nome do Banco de Dados de Distribuição**  
 Insira um nome para o banco de dados de distribuição. O nome padrão para o banco de dados de distribuição é “distribuição”. Se você especificar um nome, o nome poderá ter no máximo 128 caracteres, deve ser exclusivo em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e deve estar de acordo com as regras para identificadores. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 **Pasta para o arquivo de banco de dados de distribuição** e **Pasta para o arquivo de log de banco de dados de distribuição**  
 Insira o caminho para o banco de dados de distribuição e arquivos de log. Os caminhos devem se referir aos discos locais do Distribuidor e começar com uma letra de unidade e dois pontos (por exemplo, C:). Letras de unidades e caminhos de rede mapeados não são válidos.  
  
> [!NOTE]  
>  Você pode diminuir o tempo de gravação das transações e aprimorar o desempenho da replicação colocando o log do banco de dados de distribuição em uma unidade de disco separada do banco de dados de distribuição.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
