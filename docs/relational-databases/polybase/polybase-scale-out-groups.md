---
title: Grupos de escala horizontal do PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3fd249645266a7d9477e2dc098817138d8f722d0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34334327"
---
# <a name="polybase-scale-out-groups"></a>Grupos de escala horizontal do PolyBase
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Uma instância do SQL Server autônoma com PolyBase pode se tornar um gargalo de desempenho ao lidar com grandes conjuntos de dados no Hadoop ou no Armazenamento de Blobs do Azure. O recurso Grupo do PolyBase permite a você criar um cluster de instâncias do SQL Server para processar grandes conjuntos de dados de fontes de dados externas, como Hadoop e Armazenamento de Blobs do Azure, de maneira escalar horizontal para melhor desempenho de consulta.  
  
 Veja [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) e [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md).  
  
 ![Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups.png "Grupos de escala horizontal do PolyBase")  
  
## <a name="overview"></a>Visão geral  
  
### <a name="head-node"></a>Nó de cabeçalho  
 O nó de cabeçalho contém a instância do SQL Server para a qual as consultas do PolyBase são enviadas. Cada grupo do PolyBase pode ter apenas um nó de cabeçalho. Um nó de cabeçalho é um grupo lógico do Mecanismo de Banco de Dados do SQL, do Mecanismo de PolyBase e do Serviço de Movimentação de Dados de PolyBase na instância do SQL Server.  
  
### <a name="compute-node"></a>Nó de computação  
 Um nó de computação contém a instância do SQL Server que auxilia no processamento de consulta de escala horizontal de dados externos. Um nó de cabeçalho é um grupo lógico do SQL Server e do serviço de movimentação de dados de PolyBase na instância do SQL Server. Um grupo do PolyBase pode ter vários nós de computação.  O nó principal e os nós de computação devem executar a mesma versão do SQL Server.
  
### <a name="distributed-query-processing"></a>Processamento de consulta distribuída  
 As consultas do PolyBase são enviadas ao SQL Server no nó de cabeçalho. A parte da consulta que se refere a tabelas externas é entregue ao mecanismo de PolyBase.  
  
 O mecanismo de PolyBase é o componente principal por trás das consultas do PolyBase. Ele analisa a consulta em dados externos, gera o plano de consulta e distribui o trabalho para o serviço de movimentação de dados em nós de computação para execução. Após a conclusão do trabalho, ele recebe os resultados dos nós de computação e os envia para o SQL Server para processamento e retorno ao cliente.  
  
 O serviço de movimentação de dados do PolyBase recebe instruções do mecanismo do PolyBase e transfere dados entre o HDFS e o SQL Server, e entre instâncias do SQL Server nos nós de cabeçalho e computação.  
  
### <a name="editions-availability"></a>Disponibilidade de edições  
 Após a instalação do SQL Server, a instância poderá ser designada como um nó de cabeçalho ou um nó de computação.  A escolha depende da versão em que o PolyBase do SQL Server está em execução. Em uma instalação da edição Enterprise, a instância pode ser designada como nó de cabeçalho ou nó de computação. Em uma edição Standard, a instância pode ser designada apenas como um nó de computação.  
  
## <a name="to-configure-a-polybase-group"></a>Para configurar um grupo do PolyBase  
  
### <a name="prerequisites"></a>Prerequisites  
  
-   N computadores no mesmo domínio  
  
-   Uma conta de usuário de domínio para executar serviços do PolyBase  
  
### <a name="steps"></a>Etapas  
  
1.  Instale a mesma versão do SQL Server com PolyBase em N computadores.  
  
2.  Selecione uma instância do SQL Server como o nó de cabeçalho. Um nó de cabeçalho pode ser designado apenas em uma instância executando o SQL Server Enterprise.  
  
3.  Adicione as instâncias restantes do SQL Server como nós de computação usando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
4.  Monitore os nós no grupo usando [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).  
  
5.  Opcional. Remova um nó de computação usando [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
## <a name="example-walk-through"></a>Exemplo detalhado  
 Veja o passo a passo de como configurar um Grupo do PolyBase usando:  
  
1.  Dois computadores no domínio *PQTH4A* Os nomes de computador são:  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  Conta de domínio: *PQTH4A\PolybaseUse*r  
  
#### <a name="step-1-install-sql-server-with-polybase-on-all-machines"></a>Etapa 1: Instalar o SQL Server com PolyBase em todos os computadores  
  
1.  Execute setup.exe.  
  
2.  Na página Seleção de Recurso, escolha **Serviço de Consulta do PolyBase para Dados Externos**.  
  
3.  Na página Configuração do Servidor, use a **conta de domínio** PQTH4A\PolybaseUser para o Serviço de Movimentação de Dados do PolyBase do SQL Server e Mecanismo do PolyBase do SQL Server.  
  
4.  Na página Configuração do PolyBase, escolha a opção **Usar a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase**. Isso abre o firewall para permitir conexões de entrada para os serviços do PolyBase.  
  
5.  Depois que a instalação estiver concluída, execute **services.msc**. Verifique se o SQL Server, o Mecanismo de PolyBase e o Serviço de Movimentação de Dados de PolyBase estão em execução.  
  
     ![Serviços do PolyBase](../../relational-databases/polybase/media/polybase-services.png "Serviços do PolyBase")  
  
#### <a name="step-2-select-one-sql-server-as-head-node"></a>Etapa 2: Selecionar um SQL Server como nó de cabeçalho  
  
-   Depois que a instalação estiver concluída, os computadores podem funcionar como nós de cabeçalho do Grupo do PolyBase. Neste exemplo, podemos escolher "MSSQLSERVER" em PQTH4A CMP01 como o nó de cabeçalho.  
  
#### <a name="step-3-add-other-sql-server-instances-as-compute-nodes"></a>Etapa 3: Adicionar outras instâncias do SQL Server como nós de computação  
  
1.  Conecte-se ao SQL Server no PQTH4A CMP02.  
  
2.  Execute o procedimento armazenado [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  Execute services.msc no nó de computação (PQTH4A-CMP02).  
  
4.  Desligue o mecanismo de PolyBase e reinicie o serviço de movimentação de dados do PolyBase.  
  
#### <a name="optional-remove-a-compute-node"></a>Opcional: remover um nó de computação  
  
1.  Conecte-se ao SQL Server do nó de computação (PQTH4A CMP02).  
  
2.  Execute o procedimento armazenado sp_polybase_leave_group.  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  Execute services.msc no nó de computação que está sendo removido (PQTH4A-CMP02).  
  
4.  Inicie o Mecanismo de PolyBase. Reinicie o serviço de movimentação de dados de PolyBase.  
  
5.  Verifique se o nó foi removido executando o DMV sys.dm_exec_compute_nodes em PQTH4A-CMP01. Agora, PQTH4A-CMP02 funcionará como um nó de cabeçalho autônomo  
  
## <a name="next-steps"></a>Próximas etapas  
 Para solução de problemas, confira [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)   
 [Configuração de conectividade do PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  
