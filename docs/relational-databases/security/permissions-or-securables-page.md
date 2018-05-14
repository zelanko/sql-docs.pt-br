---
title: Página Permissões ou Protegíveis | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.permissions.f1
- sql13.swb.SecurableAndEffectPermissions.f1
- sql13.swb.common.columnperm.f1
- sql13.swb.availabilitygroupproperties.permission.f1
- sql13.swb.SecurableAndEffectivePermission.f1
ms.assetid: b3bf077a-bec2-4161-ac0c-460586199906
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ee922c02ec87f4d8908b597f694328703366cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="permissions-or-securables-page"></a>Página Permissões ou Protegíveis
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Use a página **Permissões** ou a página **Protegíveis** para exibir ou definir as permissões para protegíveis. Essa página pode ser aberta de muitos locais. O conteúdo da página pode ser ligeiramente alterado, dependendo de como a página é aberta e do que contém. A grade na parte superior da página pode estar populada quando a página é aberta ou pode estar vazia. Para adicionar itens à grade superior, clique em **Pesquisar**. Na grade superior, selecione um item e, depois, defina as permissões apropriadas na guia **Explícita** . Para exibir as permissões adicionadas, use a guia **Efetiva** .  
  
 Para entender as combinações possíveis de protegíveis e as entidades, confira os links de sintaxe específica de protegíveis no tópico [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md). Para obter mais informações, consulte [Securables](../../relational-databases/security/securables.md).  
  
## <a name="page-header"></a>Cabeçalho de página  
 O cabeçalho da página **Permissões** ou **Protegíveis** varia, dependendo do protegível ou entidade. Ele exibe informações pertinentes ao item, como seu nome.  
  
## <a name="upper-grid"></a>Grade superior  
 A grade superior contém um ou mais itens para os quais podem ser definidas permissões. Essa caixa de diálogo fornece o botão **Pesquisar** para selecionar objetos ou entidades a serem adicionados à grade superior. O nome da grade pode exibir **Protegíveis** ou um ou mais tipos de protegíveis ou entidades. As colunas que são exibidas na grade superior variam, dependendo da entidade ou protegível.  
  
 **Nome**  
 O nome de cada entidade ou protegível que é adicionado à grade.  
  
 **Tipo**  
 Descreve o tipo de cada item.  
  
## <a name="explicit-tab"></a>Guia Explícita  
 A guia **Explícita** lista as permissões possíveis para o protegível que está selecionado na grade superior. Para configurar permissões, marque ou desmarque as caixas de seleção **Conceder** (ou **Permitir**), **Com Concessão**e **Negar** . Nem todas as opções estão disponíveis para todas as permissões explícitas.  
  
 **Permissões**  
 O nome da permissão.  
  
 **Concessor**  
 A entidade que concedeu a permissão.  
  
 **Conceder**  
 Selecione para conceder essa permissão ao logon. Desmarque para revogar essa permissão.  
  
 **Com Concessão**  
 Reflete o estado da opção WITH GRANT para a permissão listada. Essa caixa é somente leitura. Para aplicar essa permissão, use a instrução [GRANT](../../t-sql/statements/grant-transact-sql.md) .  
  
 **Deny**  
 Selecione para negar essa permissão ao logon. Desmarque para revogar essa permissão.  
  
 **Permissões de Coluna**  
 Para objetos que contêm colunas (como tabelas, exibições ou funções com valor de tabela), o botão **Permissões de Coluna** abre a caixa de diálogo **Permissões de Coluna** . Nessa caixa de diálogo, você pode definir **Conceder**, **Permitir**ou **Negar** permissões em colunas individuais de uma tabela ou exibição. Essa opção não está disponível para todos os tipos de objeto ou permissões.  
  
## <a name="effective-tab"></a>Guia Efetiva  
 As permissões que uma entidade tem associadas a um protegível podem vir das permissões que são definidas para diversas entidades diferentes. Por exemplo, um logon pode receber permissões individualmente e também como um membro de um grupo. A guia **Efetiva** mostra o resultado da combinação de permissões explícitas e das permissões que são recebidas pela associação a um grupo ou função. As permissões concedidas são agregadas. Uma negação de permissão substitui todas as concessões de permissões.  
  
 **Permissões**  
 O nome da permissão.  
  
 **Coluna**  
 Os nomes de colunas que são afetadas pela permissão.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
