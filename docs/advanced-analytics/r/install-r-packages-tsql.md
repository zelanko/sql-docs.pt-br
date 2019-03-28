---
title: Use o T-SQL (CREATE EXTERNAL LIBRARY) para instalar pacotes R - serviços do SQL Server Machine Learning
description: Adicione novos pacotes do R para SQL Server 2016 R Services ou serviços SQL Server 2017 Machine Learning (no banco de dados).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b59f15ace1dc96af537486336e76a209f1c85da7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510264"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>Use o T-SQL (CREATE EXTERNAL LIBRARY) para instalar pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar novos pacotes de R em uma instância do SQL Server em que o aprendizado de máquina está habilitado. Há várias abordagens à sua escolha. Usando o T-SQL funciona melhor para os administradores de servidor que não estão familiarizados com o R.

**Aplica-se a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

O [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução torna possível adicionar um pacote ou conjunto de pacotes para uma instância ou um banco de dados sem executar R ou Python code diretamente. No entanto, esse método requer preparação de pacote e permissões de banco de dados adicionais.

+ Todos os pacotes devem estar disponíveis como um arquivo compactado local, em vez de baixado sob demanda da internet.

+ Todas as dependências devem ser identificadas pelo nome e a versão e incluídas no arquivo zip. A instrução falhará se pacotes requeridos não estão disponíveis, incluindo as dependências do pacote de downstream. 

+ Você deve ser **db_owner** ou ter a permissão CREATE EXTERNAL LIBRARY em uma função de banco de dados. Para obter detalhes, consulte [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Baixar os pacotes no formato de arquivo morto

Se você estiver instalando um único pacote, baixe o pacote em formato compactado.

Ele é mais comum para instalar vários pacotes devido a dependências do pacote. Quando um pacote requer outros pacotes, você deve verificar que todos eles são acessíveis entre si durante a instalação. É recomendável [criando um repositório local](create-a-local-package-repository-using-minicran.md) usando [miniCRAN](https://andrie.github.io/miniCRAN/) para montar um conjunto completo de pacotes, bem como [igraph](https://igraph.org/r/) para analisar as dependências de pacotes. Instalando a versão incorreta de um pacote ou omitir uma dependência de pacote pode causar uma falha da instrução CREATE EXTERNAL LIBRARY. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie o arquivo para uma pasta local

Copie o arquivo compactado que contém todos os pacotes em uma pasta local no servidor. Se você não tiver acesso ao sistema de arquivos no servidor, você também pode passar um pacote completo como uma variável, usando um formato binário. Para obter mais informações, consulte [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Execute a instrução para carregar pacotes

Abra uma **consulta** janela, usando uma conta com privilégios administrativos.

Execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

Por exemplo, a instrução a seguir nomes como origem do pacote um repositório miniCRAN que contém o **randomForest** pacote, juntamente com suas dependências. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

Você não pode usar um nome arbitrário; o nome da biblioteca externa deve ter o mesmo nome que você pretende usar ao carregar ou chamar o pacote.

## <a name="verify-package-installation"></a>Verificar a instalação do pacote

Se a biblioteca for criada com êxito, você pode executar o pacote no SQL Server, chamando-o em um procedimento armazenado.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Guias de instruções](sql-server-machine-learning-tasks.md)