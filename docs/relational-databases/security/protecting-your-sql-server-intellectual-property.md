---
title: Protegendo a propriedade intelectual do SQL Server | Microsoft Docs
description: Entenda suas opções para proteger a propriedade intelectual em um aplicativo de dados SQL Server que é distribuído para os clientes.
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4619b4bd72258e67388ee7498eff63b28a1f3b03
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869009"
---
# <a name="protecting-your-sql-server-intellectual-property"></a>Protegendo a propriedade intelectual do seu SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Os desenvolvedores de software geralmente perguntam como distribuir seus aplicativos de dados do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para os clientes e ainda evitar que os clientes de analisem e desconstruam seus aplicativos. O ponto principal aqui, é que a proteção da sua propriedade intelectual é uma questão legal e essa proteção consta no contrato de licença. Quando o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é instalado em um computador que outras pessoas administram, inerentemente você perde alguns aspectos do controle. 

## <a name="nature-of-the-problem"></a>Natureza do problema
O proprietário/administrador de um computador sempre pode acessar a instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instalada no computador. Se você implantar seu aplicativo em um computador do cliente, desde que eles sejam administradores, eles poderão se conectar ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como membros da função de servidor fixa **sysadmin**. Isso inclui a capacidade de conceder permissões, gerenciar backups (incluindo restaurar backups em outros computadores), descriptografar e mover arquivos de dados, etc. Para obter mais informações, veja [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). 

Dados e procedimentos armazenados podem ser criptografados, mas não é possível ocultar a estrutura de dados e os usuários que podem anexar um depurador ao processo do servidor podem recuperar dados e procedimentos descriptografados da memória em runtime.

Se os clientes não forem administradores nos computadores, você poderá impedir que os clientes acessem. Você pode usar a [Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md) para criptografar os arquivos de dados, pode criptografar backups e pode auditar as ações de todos os usuários. Mas os administradores do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e os administradores do computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] podem reverter essas ações.

## <a name="solution"></a>Solução
Há várias maneiras de configurar o acesso a dados pelo cliente sem instalar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no computador dos clientes. A maneira mais fácil, provavelmente, é usar o [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] para que os clientes não sejam administradores, talvez em combinação com [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Para obter mais informações sobre como começar a usar o [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], consulte [O que é o Banco de Dados SQL? Introdução ao Banco de dados SQL](/azure/sql-database/sql-database-technical-overview).  

Você também pode hospedar um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] na sua própria rede e permitir que os clientes acessem dados por meio da sua rede, diretamente ou por meio de um aplicativo Web.

## <a name="see-also"></a>Consulte Também

[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)