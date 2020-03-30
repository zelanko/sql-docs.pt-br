---
title: Segurança do SQL Server
description: Fornece uma visão geral dos recursos de segurança do SQL Server, bem como cenários de aplicativo para criar aplicativos ADO.NET seguros direcionados ao SQL Server.
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: af4e3ff43499f32d276d27873211330bc28f0cc5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896279"
---
# <a name="sql-server-security"></a>Segurança do SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O SQL Server tem muitos recursos que oferecem suporte à criação de aplicativos de banco de dados seguros.  
  
As considerações de segurança comuns são aplicáveis, como o roubo de dados ou o vandalismo, independentemente da versão do SQL Server que você está usando. A integridade dos dados também deve ser considerada um problema de segurança. Se os dados não estiverem protegidos, possivelmente se tornarão inúteis se a manipulação de dados ad hoc for permitida e os dados forem modificados inadvertida ou maliciosamente com valores incorretos ou excluídos inteiramente. Além disso, geralmente há requisitos legais que devem ser cumpridos, como o armazenamento correto de informações confidenciais. O armazenamento de alguns tipos de dados pessoais é totalmente prescrito, dependendo das leis aplicáveis em uma determinada jurisdição.  
  
Cada versão do SQL Server tem recursos de segurança diferentes, assim como cada versão do Windows, com versões mais recentes que aprimoram a funcionalidade das mais antigas. É importante entender que os recursos de segurança sozinhos não podem garantir um aplicativo de banco de dados seguro. Cada aplicativo de banco de dados é único em seus requisitos, em seu ambiente de execução, em seu modelo de implantação, em sua localização física e em sua população de usuários. Alguns aplicativos com escopo local podem precisar somente de segurança mínima, enquanto outros aplicativos locais ou aplicativos implantados pela Internet podem exigir medidas de segurança rígidas e monitoramento e avaliação contínuos.  
  
Os requisitos de segurança de um aplicativo de banco de dados do SQL Server devem ser considerados em tempo de design, não depois. A avaliação de ameaças no início do ciclo de desenvolvimento oferece a oportunidade de reduzir possíveis danos sempre que uma vulnerabilidade é detectada.  
  
Mesmo se o projeto inicial de um aplicativo estiver correto, novas ameaças poderão surgir à medida que o sistema evoluir. Com a criação de várias linhas de defesa ao redor do seu banco de dados, você poderá minimizar os danos infligidos por uma violação de segurança. Sua primeira linha de defesa é reduzir a área da superfície de ataque nunca concedendo mais permissões do que o realmente necessário.  
  
Os tópicos nesta seção descrevem resumidamente os recursos de segurança do SQL Server que são relevantes para os desenvolvedores, com links para tópicos relevantes nos Manuais Online do SQL Server e outros recursos que fornecem uma cobertura mais detalhada.  
  
## <a name="in-this-section"></a>Nesta seção  
[Autenticação no SQL Server](authentication-sql-server.md)  
Descreve logons e a autenticação no SQL Server e fornece links para recursos adicionais. 
  
[Cenários de segurança de aplicativo no SQL Server](application-security-scenarios-sql-server.md)  
Contém os tópicos que abordam vários cenários de segurança de aplicativos para o ADO.NET e aplicativos do SQL Server.  
  
[Segurança do SQL Server Express](sql-server-express-security.md)  
Descreve considerações de segurança para o SQL Server Express.  
  
## <a name="related-sections"></a>Seções relacionadas  
[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
Descreve as considerações de segurança para o SQL Server e o Banco de Dados SQL do Azure.

[Considerações sobre segurança para uma instalação do SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
Descreve as preocupações de segurança a serem consideradas antes de instalar o SQL Server.

## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
