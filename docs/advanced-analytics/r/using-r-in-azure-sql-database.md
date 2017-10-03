---
title: Usando o R no banco de dados SQL do Azure | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: pt-br
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>Usando o R no banco de dados SQL do Azure

A partir de outubro de 2017, o banco de dados SQL dá suporte à execução de R código no banco de dados usando procedimentos armazenados, semelhantes aos serviços do R no SQL Server 2016.

Este artigo fornece uma visão geral do recurso e descreve as restrições conhecidas.

> [!NOTE]
> Esta versão é uma versão de visualização inicial e destina-se para teste e exploração apenas. Uma versão de produção será lançada em algum momento no 2018. A data de lançamento exato e a compilação serão com base nos comentários do usuário. portanto recomendamos que você tente o recurso e queremos saber quais recursos são importantes. 
> 
> Para obter informações sobre o cronograma de lançamento, consulte o [blog do SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/) ou [blog do Microsoft R Server](https://blogs.msdn.microsoft.com/rserver/).

## <a name="features"></a>Recursos

A versão de visualização fornece a seguinte funcionalidade:

+ Chamar o R usando procedimentos armazenados para facilitar a implantação de soluções de aprendizado de máquina
+ Obter pontuações do modelo usando qualquer aplicativo que pode se conectar ao seu banco de dados de nuvem
+ Oferece suporte nativo de pontuação usando a função de previsão, para pontuação rápida sem o uso de tempo de execução de R

Para restrições específicas para a versão de visualização, consulte [restrições e problemas conhecidos](#bkmk_restrictions).

### <a name="components"></a>Componentes

A arquitetura geral é semelhante de máquina do SQL Server R Services.

**Segurança**

+ O Launchpad do SQL Server confiável gerencia a execução de trabalhos de R e controla o tempo de vida de processos. 

**Pacotes de R**

+ A versão de preview inclui o Microsoft R Open 3.3.3 e Microsoft R Server versão 9.2. O [pacote RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) foi pré-instalado.

+ Alguns pacotes de R foram removidas ou modificadas para reduzir o volume no ambiente do Azure. Por exemplo, **mrsdeploy** não está incluído no banco de dados do SQL Azure.

**Desempenho**

+ Dá suporte a treinamento e pontuação de qualquer modelo onde os dados podem caber na memória.  A quantidade de memória disponível depende da edição do banco de dados. 
+ Há suporte para paralelismo trivial usando o @parallel = 1 argumento, bem como para a execução de script R de streaming 
+ Na visualização, limitado a um único script R executado simultaneamente por banco de dados.

**Idiomas**

O mapa para versão futura inclui suporte para pacotes adicionais e Python.

## <a name="restrictions"></a>Restrições

Esta seção lista algumas limitações adicionais que se aplicam à versão de visualização.

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>Atualizando componentes de R e adição de pacotes não tem suportados

Banco de dados do SQL Azure é um serviço gerenciado, e os clientes não são esperados para gerenciar atualizações para os componentes de R. Para a versão de visualização, use os pacotes instalados disponíveis.

Atualizações para o R e outros componentes de aprendizado de máquina serão liberadas assim que estiverem disponíveis.

### <a name="availability"></a>Disponibilidade

A capacidade de executar R e outros scripts no SQL Azure de aprendizado de máquina é um recurso de visualização na Central Oeste dos EUA região somente. Expansão de outras regiões, como Europa Ocidental, está planejado para versões posteriores.

Executar R no SQL Azure requer armazenamento e memória suficientes. Atualmente, são suportados os seguintes níveis de serviço de banco de dados e níveis de desempenho:

+ Camada de serviço Premium: P1, P2, P4, P6, P11, P15 
+ Camada de serviço RS Premium: PRS1, PRS2, PRS4, PRS6 
+ Pool Elástico do Premium: eDTUs 125 ou maior 
+ Pool de RS Elástico Premium: eDTUs 125 ou maior 

### <a name="resource-management"></a>Gerenciamento de recursos

Esta versão não dá suporte a capacidade de personalizar a instalação de R, ou para monitorar o uso de scripts de R.

Por exemplo, você não pode habilitar a execução do script R somente em bancos de dados específicos.

O DMV sys.DM db_resource_stats, usado para monitorar o uso de CPU e memória de scripts de R, não está disponível na versão de visualização.

### <a name="other-limitations"></a>Outras limitações

Não há suporte para a seguinte funcionalidade: 

+ O pacote de MicrosoftML não está disponível.
+ Não há suporte para recursos de gerenciamento de pacotes como criar biblioteca externa.
+ Você não pode usar o banco de dados do SQL Azure como um contexto de computação remoto durante a execução de scripts de um cliente de R. Scripts R devem ser executados usando o procedimento armazenado sp_execute_external_script. Scripts chamados pelo procedimento armazenado não é possível usar outros contextos de computação.
+ Você não pode executar as chamadas para funções de rx que exigem a execução paralela.
+ Não há suporte para conexões de loopback de script R para o SQL Server. Em outras palavras, você não pode fazer chamadas externas de seu script R para outra fonte de dados ODBC.

## <a name="get-started"></a>Introdução

Este lançamento da equipe de desenvolvimento do SQL Server inclui exemplos curtos que podem ser executados em seus próprios bancos de dados SQL do Azure para fazer experiências com a criação de modelos de R e gerar previsões.

+ [Treinar e pontuar os modelos no banco de dados SQL do Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

