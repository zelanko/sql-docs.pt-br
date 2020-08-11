---
title: Importar para um projeto de banco de dados
description: Saiba como importar objetos para um projeto de banco de dados de um banco de dados dinâmico, um aplicativo da camada de dados e um script. Saiba mais sobre como importar objetos criptografados.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLPROJECTIMPORTSNAPSHOTSUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.SQLPROJECTIMPORTDATABASESUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.IMPORTSCRIPTWIZARD.SUMMARY
ms.assetid: d0a0a394-6cb6-416a-a25f-9babf8ba294a
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 9cbe1d734238728b87f6931fdee49654155e82e6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893865"
---
# <a name="import-into-a-database-project"></a>Importar para um projeto de banco de dados

Você pode usar Importar para popular um projeto com novos objetos de um banco de dados dinâmico ou um .dacpac, ou para atualizar objetos existentes no seu projeto com uma nova definição de um script. Há algumas diferenças de comportamento que devem ser observadas entre esses três caminhos, que são descritas a seguir.  
  
**Menu Importar**  
  
![Menu Importar do SSDT](../ssdt/media/ssdt-import.gif "Menu Importar do SSDT")  
  
**Seções neste tópico**  
  
[Origem da Importação: Banco de dados ou aplicativo da camada de dados (*.dacpac)](#bkmk_import_source_db)  
  
[Origem da Importação: Script (*.sql)](#bkmk_import_source_script)  
  
[Importar objetos criptografados](#bkmk_import_encrypted)  
  
## <a name="import-source-database-or-data-tier-application-dacpac"></a><a name="bkmk_import_source_db"></a>Origem da Importação: Banco de dados ou aplicativo da camada de dados (*.dacpac)  
A capacidade de importar o esquema de um banco de dados ou um arquivo .dacpac somente estará disponível se não houver objetos de esquema já definidos no projeto. Isso não inclui RefactorLogs ou scripts de pré/pós-implantação.  
  
Durante a importação, as definições de objeto serão colocadas em scripts nos arquivos de projeto usando os padrões organizacionais do SSDT para novos objetos: novos arquivos para objetos de nível superior, filhos hierárquicos definidos no mesmo arquivo como o pai, restrições de tabela/coluna definidas de modo embutido quando possível. Para obter a visibilidade e o controle mais direcionados para cada objeto, use Comparação de Esquemas, em vez de Importar.  
  
Se a fonte de importação contiver Scripts Pré e Pós-Implantação, RefactorLogs ou definições de variáveis SQLCMD, eles serão importados para o projeto. Se o projeto já contiver um desses artefatos, os arquivos importados serão adicionados a uma pasta **Ignorados na Importação** no projeto.  
  
**Pasta Ignorados na Importação**  
  
![Pasta Ignorados na Importação do SSDT](../ssdt/media/ssdt-ignoredonimport.gif "Pasta Ignorados na Importação do SSDT")  
  
## <a name="import-source-script-sql"></a><a name="bkmk_import_source_script"></a>Origem da Importação: Script (*.sql)  
Todos os objetos da fonte de importação que ainda *não* existirem no projeto serão adicionados e todos os objetos na fonte de importação que *já* existirem no projeto substituirão a definição de objeto no projeto.  
  
> [!NOTE]  
> Há dois bugs conhecidos nesse caminho que serão corrigidos em uma versão futura:  
>   
> -   Se restrições de tabela/coluna forem definidas fora da instrução CREATE TABLE na definição de tabela do projeto, a importação substituirá a definição de tabela de modo que a restrição fique embutida. No entanto, isso deixará a restrição fora de linha, resultando em restrições duplicadas no projeto.  
> -   Qualquer chave mestra ou chave de criptografia de banco de dados do seu script de origem que já exista no projeto será duplicada na importação. Remova as duplicatas para compilar o projeto.  
  
O processo Importar do Script não incluirá scripts Pré/Pós-Implantação, variáveis SQLCMD ou arquivos RefactorLog. Esses e qualquer outra construção sem suporte que seja detectada na importação serão colocados em um arquivo **ScriptsIgnoredOnImport.sql** em uma pasta **Scripts** no seu projeto.  
  
 
## <a name="import-encrypted-objects"></a><a name="bkmk_import_encrypted"></a>Importar objetos criptografados  
Ao importar objetos criptografados para um projeto de banco de dados, nem sempre será possível recuperar todo o corpo da definição de objeto do servidor. Assim, o comportamento de importação poderá ser diferente ao lidar com essa classe de objetos.  
  
Quando não for possível recuperar a definição de corpo total, será criado um script com o cabeçalho/rodapé de objeto junto com um corpo fictício. Você pode esperar encontrar esse comportamento ao Importar ou usar Comparação de Esquemas em que a fonte for um banco de dados dinâmico ou um .dacpac extraído de um banco de dados.  
  
**Script com corpo fictício**  
  
![Script com um corpo fictício](../ssdt/media/ssdt-procwithencryption.gif "Script com um corpo fictício")  
  
No caso em que a definição de objeto completa está disponível e pode ser recuperada, Importar e Comparação de Esquemas a colocarão completa no projeto. Isso ocorre durante a atualização do projeto a partir de um script, um .dacpac criado a partir de um projeto de banco de dados ou outro projeto de banco de dados.  
  
