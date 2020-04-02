---
title: Configurar grupos de escala horizontal do PolyBase no Windows | Microsoft Docs
description: Configure um grupo de escala horizontal do PolyBase para criar um cluster de instâncias do SQL Server. Isso aprimora o desempenho de consulta para grandes conjuntos de dados de fontes externas.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: tutorial
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 658dcbccb515b7d5d720d0bb0c677aa2178b7606
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80216075"
---
# <a name="configure-polybase-scale-out-groups-on-windows"></a>Configurar grupos de escala horizontal do PolyBase no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como configurar um [Grupo de escala horizontal do PolyBase](polybase-scale-out-groups.md) no Windows. Isso cria um cluster de instâncias do SQL Server para processar grandes conjuntos de dados de fontes de dados externas, como Hadoop e Armazenamento de Blobs do Azure, de maneira expandir para melhor desempenho de consulta.

## <a name="prerequisites"></a>Pré-requisitos
  
- Mais de um computador no mesmo domínio  
  
- Uma conta de usuário de domínio para executar serviços do PolyBase  
  
## <a name="process-overview"></a>Visão geral do processo

As etapas a seguir resumem o processo de criação de um grupo de expansão do PolyBase. A próxima seção fornece uma explicação mais detalhada de cada etapa.
  
1. Instale a mesma versão do SQL Server com PolyBase em N computadores.
  
2. Selecione uma instância do SQL Server como o nó de cabeçalho. Um nó de cabeçalho pode ser designado apenas em uma instância executando o SQL Server Enterprise.
  
3. Adicione as instâncias restantes do SQL Server como nós de computação usando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

4. Monitore os nós no grupo usando [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).

5. Opcional. Remova um nó de computação usando [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).

## <a name="example-walk-through"></a>Exemplo detalhado

Veja o passo a passo de como configurar um Grupo do PolyBase usando:  
  
1. Dois computadores no domínio *PQTH4A* Os nomes de computador são:  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. Conta de domínio: *PQTH4A\PolyBaseUse*r  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>Instalar o SQL Server com PolyBase em todos os computadores

1. Execute setup.exe.
  
2. Na página Seleção de Recursos, escolha **Serviço de Consulta do PolyBase para Dados Externos**.
  
3. Na página Configuração do Servidor, use a **conta de domínio** PQTH4A\PolyBaseUser para o Mecanismo PolyBase do SQL Server e o Serviço de Movimentação de Dados PolyBase do SQL Server.
  
4. Na página Configuração do PolyBase, escolha a opção **Usar a instância do SQL Server como parte de um grupo de escala horizontal do PolyBase**. Isso abre o firewall para permitir conexões de entrada para os serviços do PolyBase. Caso o nó principal seja uma instância nomeada, será necessário adicionar manualmente a porta do SQL Server ao Firewall do Windows e iniciar o SQL Browser no nó principal.
  
5. Depois que a instalação estiver concluída, execute **services.msc**. Verifique se o SQL Server, o Mecanismo de PolyBase e o Serviço de Movimentação de Dados de PolyBase estão em execução.
  
   ![Serviços PolyBase](../../relational-databases/polybase/media/polybase-services.png "Serviços PolyBase")  
  
## <a name="select-one-sql-server-as-head-node"></a>Selecione um SQL Server como nó de cabeçalho  
  
Depois que a instalação estiver concluída, os computadores podem funcionar como nós de cabeçalho do Grupo do PolyBase. Neste exemplo, podemos escolher "MSSQLSERVER" em PQTH4A-CMP01 como o nó de cabeçalho.
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>Adicionar outras instâncias do SQL Server como nós de computação  
  
1. Conecte-se ao SQL Server no PQTH4A CMP02.
  
2. Execute o procedimento armazenado [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. Execute services.msc no nó de computação (PQTH4A-CMP02).
  
4. Desligue o mecanismo de PolyBase e reinicie o serviço de movimentação de dados do PolyBase.
  
## <a name="optional-remove-a-compute-node"></a>Opcional: remover um nó de computação  
  
1. Conecte-se ao SQL Server do nó de computação (PQTH4A CMP02).
  
2. Execute o procedimento armazenado sp_polybase_leave_group.
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. Execute services.msc no nó de computação que está sendo removido (PQTH4A-CMP02).
  
4. Inicie o Mecanismo de PolyBase. Reinicie o serviço de movimentação de dados de PolyBase.
  
5. Verifique se o nó foi removido executando o DMV sys.dm_exec_compute_nodes em PQTH4A-CMP01. Agora, PQTH4A-CMP02 funcionará como um nó de cabeçalho autônomo  
  
## <a name="next-steps"></a>Próximas etapas  

Para solução de problemas, confira [PolyBase troubleshooting with dynamic management views](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).
  
Para obter mais informações sobre o PolyBase, consulte [Visão geral do PolyBase](../../relational-databases/polybase/polybase-guide.md).
