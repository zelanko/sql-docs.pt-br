---
title: Segurança do SQL Server
description: Fornece uma visão geral dos recursos de segurança do SQL Server, bem como cenários de aplicativo para criar aplicativos ADO.NET seguros direcionados ao SQL Server.
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: bb9e02743122958cb567e01f5011fc9f8b3481e6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452001"
---
# <a name="sql-server-security"></a>Segurança do SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O SQL Server tem muitos recursos que oferecem suporte à criação de aplicativos de banco de dados seguros.  
  
As considerações de segurança comuns são aplicáveis, como o roubo de dados ou o vandalismo, independentemente da versão do SQL Server que você está usando. A integridade dos dados também deve ser considerada como um problema de segurança. Se os dados não estiverem protegidos, será possível que ele se torne inúteis se a manipulação de dados ad hoc for permitida e os dados forem modificados inadvertidamente ou maliciosamente com valores incorretos ou excluídos inteiramente. Além disso, geralmente há requisitos legais que devem ser cumpridos, como o armazenamento correto de informações confidenciais. O armazenamento de alguns tipos de dados pessoais é totalmente inscrito, dependendo das leis que se aplicam em uma jurisdição específica.  
  
Cada versão do SQL Server tem recursos de segurança diferentes, assim como cada versão do Windows, com versões mais recentes que aprimoram a funcionalidade das mais antigas. É importante entender que os recursos de segurança sozinhos não podem garantir um aplicativo de banco de dados seguro. Cada aplicativo de banco de dados é exclusivo em seus requisitos, ambiente de execução, modelo de implantação, local físico e população de usuário. Alguns aplicativos que são locais no escopo podem precisar apenas de segurança mínima, enquanto outros aplicativos ou aplicativos locais implantados pela Internet podem exigir medidas de segurança rígidas e monitoramento e avaliação contínuas.  
  
Os requisitos de segurança de um aplicativo de banco de dados do SQL Server devem ser considerados em tempo de design, não depois. A avaliação de ameaças no início do ciclo de desenvolvimento oferece a oportunidade de reduzir possíveis danos sempre que uma vulnerabilidade for detectada.  
  
Mesmo que o design inicial de um aplicativo seja bom, novas ameaças podem surgir à medida que o sistema evolui. Ao criar várias linhas de defesa em todo o banco de dados, você pode minimizar os danos causados por uma violação de segurança. Sua primeira linha de defesa é reduzir a área da superfície de ataque para nunca conceder mais permissões do que as absolutamente necessárias.  
  
Os tópicos nesta seção descrevem resumidamente os recursos de segurança do SQL Server que são relevantes para os desenvolvedores, com links para tópicos relevantes nos Manuais Online do SQL Server e outros recursos que fornecem uma cobertura mais detalhada.  
  
## <a name="in-this-section"></a>Nesta seção  
[Autenticação no SQL Server](authentication-sql-server.md)  
Descreve os logons e a autenticação no SQL Server e fornece links para recursos adicionais. 
  
[Cenários de segurança de aplicativo no SQL Server](application-security-scenarios-sql-server.md)  
Contém os tópicos que abordam vários cenários de segurança de aplicativos para o ADO.NET e aplicativos do SQL Server.  
  
[Segurança do SQL Server Express](sql-server-express-security.md)  
Descreve as considerações de segurança para SQL Server Express.  
  
## <a name="related-sections"></a>Seções relacionadas  
[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
Descreve as considerações de segurança para o SQL Server e o banco de dados SQL do Azure.

[Considerações sobre segurança para uma instalação do SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
Descreve as questões de segurança a considerar antes de instalar o SQL Server.

## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
