---
title: Testar objetos de banco de dados (SybaseToSQL) migrados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ac7654f43f2d453ad0e55a0a7ebcfee79ac2c91c
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393339"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Testar objetos de banco de dados migrados (SybaseToSQL)
Microsoft SQL Server Migration Assistant for Sybase testador (SSMA testador) testa automaticamente a conversão do objeto de banco de dados e a migração de dados feitas por SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma maneira e que todos os dados foi transferido corretamente.  
  
> [!NOTE]  
> Componente do testador está desabilitado no caso de conectividade do Azure.  
  
Você pode testar os seguintes tipos de objeto com o SSMA testador:  
  
-   Tabelas  
  
-   Procedimentos armazenados  
  
-   Exibições.  
  
-   Instruções de autônomo.  
  
O SSMA testador executa objetos selecionados para um teste no Sybase e suas contrapartes no SQL Server. Depois disso, ele compara os resultados de acordo com os seguintes critérios:  
  
-   As alterações nos dados de tabela são idênticos?  
  
-   Os valores de parâmetros de saída para procedimentos e funções são idênticos?  
  
-   As funções retornam os mesmos resultados?  
  
-   São que os conjuntos de resultados idênticos?  
  
> [!NOTE]  
> Atenção! Nunca use testador SSMA em sistemas de produção. Durante a execução do testador o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Prerequisites  
Se você quiser usar o testador SSMA, instale o pacote de extensão do SSMA Sybase com os **instalar o banco de dados do testador** opção ativada.  
  
Além disso, verifique o seguinte:  
  
-   Provedor do OLE DB para Sybase está instalado no computador onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
-   Integração de Common Language Runtime (CLR) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do testador do SSMA não suporta a execução paralela por usuários diferentes no mesmo servidor de origem ou destino.  
  
## <a name="getting-started"></a>Introdução  
[Criando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Instalar os componentes do SSMA no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
