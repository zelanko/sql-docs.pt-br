---
title: Protegendo a propriedade intelectual do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
caps.latest.revision: "3"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 363fa4744ca429f19e2c8dd2375146e616e85f85
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="protecting-your-sql-server-intellectual-property"></a>Protegendo a propriedade intelectual do seu SQL Server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Os desenvolvedores de software geralmente perguntam como distribuir seus aplicativos de dados do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para os clientes e ainda evitar que os clientes de analisem e desconstruam seus aplicativos. O ponto principal aqui, é que a proteção da sua propriedade intelectual é uma questão legal e essa proteção consta no contrato de licença. Quando o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é instalado em um computador que outras pessoas administram, inerentemente você perde alguns aspectos do controle. 

## <a name="nature-of-the-problem"></a>Natureza do problema
O proprietário/administrador de um computador sempre pode acessar a instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instalada no computador. Se você implantar seu aplicativo em um computador do cliente, desde que eles sejam administradores, eles poderão se conectar ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como membros da função de servidor fixa **sysadmin**. Isso inclui a capacidade de conceder permissões, gerenciar backups (incluindo restaurar backups em outros computadores), descriptografar e mover arquivos de dados, etc. Para obter mais informações, veja [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). 

Dados e procedimentos armazenados podem ser criptografados, mas não é possível ocultar a estrutura de dados e os usuários que podem anexar um depurador ao processo do servidor podem recuperar dados e procedimentos descriptografados da memória em tempo de execução.

Se os clientes não forem administradores nos computadores, você poderá impedir que os clientes acessem. Você pode usar a [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md) para criptografar os arquivos de dados, pode criptografar backups e pode auditar as ações de todos os usuários. Mas os administradores do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e os administradores do computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] podem reverter essas ações.

## <a name="solution"></a>Solução
Há várias maneiras de configurar o acesso a dados pelo cliente sem instalar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no computador dos clientes. A maneira mais fácil, provavelmente, é usar o [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] para que os clientes não sejam administradores, talvez em combinação com [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Para obter mais informações sobre como começar a usar o [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], consulte [O que é o Banco de Dados SQL? Introdução ao Banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview).  

Você também pode hospedar um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] na sua própria rede e permitir que os clientes acessem dados por meio da sua rede, diretamente ou por meio de um aplicativo Web.

## <a name="see-also"></a>Consulte também

[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  

