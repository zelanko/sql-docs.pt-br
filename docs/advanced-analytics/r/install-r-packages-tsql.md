---
title: Use T-SQL (criar biblioteca externa) para instalar pacotes R nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
description: Adicionar novos pacotes de R para serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7a5a0c394e9a26244661a4ae712d20583c1f1c99
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585478"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>Use T-SQL (criar biblioteca externa) para instalar pacotes R nos serviços de aprendizado de máquina do SQL Server de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado. Há várias abordagens para escolher. Usando o T-SQL funciona melhor para os administradores de servidor que não estão familiarizados com R.

**Aplica-se a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

O [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução, é possível adicionar um pacote ou conjunto de pacotes para uma instância ou um banco de dados sem executar R ou Python code diretamente. No entanto, esse método requer permissões de banco de dados adicionais e preparação de pacote.

+ Todos os pacotes devem estar disponível como um arquivo compactado local, em vez de download sob demanda da internet.

+ Todas as dependências devem ser identificadas pelo nome e a versão e incluídas no arquivo zip. A instrução falhará se pacotes requeridos não estão disponíveis, incluindo as dependências do pacote de downstream. 

+ Você deve ser **db_owner** ou ter a permissão de criar biblioteca externa em uma função de banco de dados. Para obter detalhes, consulte [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Baixe os pacotes no formato de arquivo

Se você estiver instalando um único pacote, baixe o pacote em formato compactado.

É mais comum para instalar vários pacotes devido a dependências do pacote. Quando um pacote requer outros pacotes, você deve verificar se todos eles estão acessíveis entre si durante a instalação. É recomendável [criando um repositório local](create-a-local-package-repository-using-minicran.md) usando [miniCRAN](http://andrie.github.io/miniCRAN/) para montar um conjunto completo de pacotes, bem como [igraph](http://igraph.org/r/) para análise de dependências de pacotes. Instalar a versão incorreta de um pacote ou omitindo uma dependência de pacote pode causar uma falha da instrução Criar biblioteca externa. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie o arquivo para uma pasta local

Copie o arquivo compactado que contém todos os pacotes em uma pasta local no servidor. Se você não tiver acesso ao sistema de arquivos no servidor, você também pode passar um pacote completo como uma variável, usando um formato binário. Para obter mais informações, consulte [criar biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Execute a instrução para carregar pacotes

Abra um **consulta** janela, usando uma conta com privilégios administrativos.

Execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

Por exemplo, a instrução a seguir nomes como a origem do pacote um repositório de miniCRAN que contém o **randomForest** pacote, juntamente com suas dependências. 

```SQL
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

Você não pode usar um nome arbitrário; o nome da biblioteca externa deve ter o mesmo nome que você pretende usar ao carregar ou chamar o pacote.

## <a name="verify-package-installation"></a>Verificar a instalação do pacote

Se a biblioteca é criada com êxito, você pode executar o pacote no SQL Server, chamando-o dentro de um procedimento armazenado.
    
```SQL
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Guias de instruções](sql-server-machine-learning-tasks.md)