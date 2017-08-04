---
title: Testando migrados objetos de banco de dados (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: db60668fb90aec8b093938533487a6f0ff5bdf0f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Testando migrados objetos de banco de dados (SybaseToSQL)
Microsoft SQL Server Migration Assistant para Sybase testador (SSMA Tester) testa automaticamente a conversão do objeto de banco de dados e a migração de dados feitas pelo SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma forma e que todos os dados foi transferido corretamente.  
  
> [!NOTE]  
> Componente de teste está desabilitado no caso de conectividade do Azure.  
  
Você pode testar os seguintes tipos de objeto com o SSMA testador:  
  
-   Tabelas  
  
-   Procedimentos armazenados  
  
-   Exibições.  
  
-   Instruções de autônomo.  
  
O SSMA Tester executa objetos selecionados para teste em Sybase e suas contrapartes no SQL Server. Depois disso, ele compara os resultados de acordo com os critérios a seguir:  
  
-   As alterações nos dados de tabela são idênticos?  
  
-   Os valores de parâmetros de saída para procedimentos e funções são idênticos?  
  
-   Funções retornam os mesmos resultados?  
  
-   São que os conjuntos de resultados idêntico?  
  
> [!NOTE]  
> Atenção! Nunca use SSMA testador em sistemas de produção. Durante a execução de teste, o esquema de origem e os dados são modificados. Enquanto isso, a restauração completa do estado original pode ser impossível para alguns tipos de código testado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Se você quiser usar o testador SSMA, instale o pacote de extensão do SSMA Sybase com os **instalar o banco de dados Tester** opção ativada.  
  
Além disso, verifique o seguinte:  
  
-   Provedor OLE DB para Sybase está instalado no computador onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é executado.  
  
-   Integração do Common Language Runtime (CLR) foi habilitada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mecanismo de banco de dados.  
  
Observe que a versão atual do SSMA Tester não suporta a execução paralela por usuários diferentes no mesmo servidor de origem ou de destino.  
  
## <a name="getting-started"></a>Guia de Introdução  
[Criar casos de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Instalando componentes do SSMA SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Configurações de projeto &#40; Conversão de &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  

