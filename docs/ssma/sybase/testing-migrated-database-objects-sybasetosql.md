---
description: Testar objetos de banco de dados migrados (SybaseToSQL)
title: Testando objetos de banco de dados migrados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cfe57d436eac38052542eb2ed6c2133aab7ca07b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480381"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Testar objetos de banco de dados migrados (SybaseToSQL)
O Assistente de Migração do Microsoft SQL Server para o Sybase Tester (SSMA Tester) testa automaticamente a conversão de objetos de banco de dados e a migração feita pelo SSMA. Depois que todas as etapas de migração do SSMA forem concluídas, use o SSMA Tester para verificar se os objetos convertidos funcionam da mesma maneira e se todos os dados foram transferidos corretamente.  
  
> [!NOTE]  
> O componente testador está desabilitado no caso da conectividade do Azure.  
  
Você pode testar os seguintes tipos de objeto com o SSMA Tester:  
  
-   Tabelas  
  
-   Procedimentos armazenados  
  
-   Exibições.  
  
-   Instruções autônomas.  
  
O SSMA Tester executa objetos selecionados para teste no Sybase e em suas contrapartes no SQL Server. Depois disso, ele compara os resultados de acordo com os seguintes critérios:  
  
-   As alterações nos dados da tabela são idênticas?  
  
-   Os valores dos parâmetros de saída para procedimentos e funções são idênticos?  
  
-   As funções retornam os mesmos resultados?  
  
-   Os conjuntos de resultados são idênticos?  
  
> [!NOTE]  
> Atenção! Nunca use o SSMA Tester em sistemas de produção. Durante a execução do testador, o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Se você quiser usar o SSMA Tester, instale o SSMA Sybase Extension Pack com a opção **instalar banco de dados do testador** ativada.  
  
Além disso, verifique o seguinte:  
  
-   O provedor de OLE DB do Sybase está instalado no computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
-   A integração CLR (Common Language Runtime) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do SSMA Tester não oferece suporte à execução paralela por diferentes usuários no mesmo servidor de origem ou de destino.  
  
## <a name="getting-started"></a>Introdução  
[Criando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Instalando os componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
