---
title: Usar certificados para um ponto de extremidade de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e1635e680fcd68de1f4877a1ffc713e526e862ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050616"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>Usar certificados para um ponto de extremidade de espelhamento de banco de dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para habilitar a autenticação de certificado para espelhamento de banco de dados em uma determinada instância do servidor, o administrador do sistema deve configurar cada instância do servidor para usar certificados nas conexões de saída e de entrada. As conexões de saída devem ser configuradas primeiro.  
  
> [!NOTE]  
>  Todas as conexões de espelhamento em uma instância do servidor usam um único ponto de extremidade de espelhamento do banco de dados e você deve especificar o método de autenticação da instância do servidor quando criar o ponto de extremidade. Portanto, você pode usar somente um formulário de autenticação por instância do servidor para espelhamento de banco de dados.  
  
## <a name="configuring-outbound-connections"></a>Configurando conexões de saída  
 Siga essas etapas em cada instância do servidor que você está configurando para espelhamento de banco de dados:  
  
1.  No banco de dados **mestre** , crie uma chave mestra de banco de dados.  
  
2.  No banco de dados **mestre** , crie um certificado criptografado na instância de servidor.  
  
3.  Crie um ponto de extremidade para a instância do servidor que usa seu certificado.  
  
4.  Faça o backup do certificado em um arquivo e o copie-o com segurança para outro sistema ou sistemas.  
  
 Você deve completar essas etapas para cada parceiro e para a testemunha, se houver.  
  
 Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
## <a name="configuring-inbound-connections"></a>Configurando conexões de saída  
 A seguir, siga estas etapas para cada parceiro que você está configurando para espelhamento de banco de dados. No banco de dados **mestre** :  
  
1.  Crie um logon para o outro sistema.  
  
2.  Crie um usuário para aquele logon.  
  
3.  Obtenha o certificado para o ponto de extremidade de espelhamento da outra instância do servidor.  
  
4.  Associe o certificado ao usuário criado na etapa 2.  
  
5.  Conceda permissão CONNECT no logon para aquele ponto de extremidade de espelhamento.  
  
 Se houver uma testemunha, deve-se configurar também conexões de entrada para ela. Isso requer configuração de logons, usuários e certificados para a testemunha nos dois parceiros, e vice-versa.  
  
 Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md).  
  
## <a name="security"></a>Segurança  
 A menos que você possa garantir que sua rede está segura, recomendamos o uso de criptografia para conexões de espelhamento de banco de dados. Para obter mais informações, consulte [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 Ao copiar um certificado para outro sistema, use um método de cópia seguro. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma chave mestra de banco de dados](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
