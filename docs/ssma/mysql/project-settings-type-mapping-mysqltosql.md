---
title: Configurações do projeto (mapeamento de tipo) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7add1259778bf189c981d5b302e989bf7bc233c3
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396556"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>Configurações do projeto (mapeamento de tipo) (MySQLToSQL)
As configurações do projeto de mapeamento de tipo permitem que você defina mapeamentos de tipo padrão para o projeto do SSMA.  

O mapeamento de tipo está disponível nas caixas de diálogo Configurações do projeto e configurações padrão do projeto:  
  
-   Use a caixa de diálogo Configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo, no menu ferramentas, selecione configurações do projeto e, em seguida, clique em mapeamento de tipo no painel esquerdo.  
  
-   Use a caixa de diálogo Configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar as configurações de mapeamento de tipo, no menu ferramentas, selecione configurações de projeto padrão, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas/Changed do menu suspenso **versão de destino de migração** e clique em mapeamento de tipo no painel esquerdo.  
  
## <a name="options"></a>Opções  
  
##### <a name="source-type"></a>Tipo de Fonte  
É o tipo de dados do MySQL, que deve ser mapeado para o tipo de dados do banco de dado de destino.  
  
##### <a name="target-type"></a>Tipo de destino  
O tipo de dado do banco de dados de destino para o tipo de dados MySQL especificado.  
  
##### <a name="add"></a>Adicionar  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
##### <a name="edit"></a>Editar  
Clique para editar o tipo de dados selecionado na lista mapeamento.  
  
##### <a name="remove"></a>Remover  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
##### <a name="reset-to-default"></a>Restaurar Padrões  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="type-mappings"></a>Mapeamentos de tipo  
A tabela a seguir mostra o mapeamento padrão entre os tipos de dados de origem e de destino  
  
|Tipo de dados MySQL|Tipo de dados do SQL Server|  
|-|-|  
|BIGINT|BIGINT|  
|bigint [*.. 255]|BIGINT|  
|binary|binário [1]|  
|binário [0.. 1]|binário [1]|  
|binário [2.. 255]|binário [*]|  
|bit|binário [1]|  
|bit [0.. 8]|binário [1]|  
|bit [17.. 24]|binário [3]|  
|bit [25.. 32]|binário [4]|  
|bit [33.. 40]|binário [5]|  
|bit [41.. 48]|binário [6]|  
|bit [49.. 56]|binário [7]|  
|bit [57.. 64]|binário [8]|  
|bit [9.. 16]|binário [2]|  
|blob|varbinary(max)|  
|Blob [0.. 1]|varbinary [1]|  
|Blob [2.. 8000]|varbinary [*]|  
|Blob [8001.. *]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar [1]|  
|byte de caracteres|binário [1]|  
|byte de caractere [0.. 1]|binário [1]|  
|byte de caractere [2.. 255]|binário [*]|  
|caractere [0.. 1]|nchar [1]|  
|caractere [2.. 255]|nchar [*]|  
|character|nchar [1]|  
|variação de caractere [0.. 1]|nvarchar [1]|  
|variação de caractere [2.. 255]|NVARCHAR|  
|caractere [0.. 1]|nchar [1]|  
|caractere [2.. 255]|nchar [*]|  
|date|date|  
|DATETIME|datetime2 [0]|  
|dec|decimal|  
|Dec [*.. 65]|Decimal [*] [0]|  
|Dec [*.. 65] [ \* .. máximo|Decimal [*] [ \* ]|  
|decimal|decimal|  
|Decimal [*.. 65]|Decimal [*] [0]|  
|Decimal [*.. 65] [ \* .. máximo|Decimal [*] [ \* ]|  
|double|float [53]|  
|double precision|float [53]|  
|precisão dupla [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|Duplo [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|fixo|numeric|  
|Corrigido [*.. 65] [ \* .. máximo|numeric [*] [ \* ]|  
|FLOAT|float [24]|  
|float [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|float [*.. 53]|float [53]|  
|INT|INT|  
|int [*.. 255]|INT|  
|inteiro|INT|  
|inteiro [*.. 255]|INT|  
|longblob|varbinary(max)|  
|longtext|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|INT|  
|mediumint[*.. 255]|INT|  
|mediumtext|nvarchar(max)|  
|caractere nacional|nchar [1]|  
|caractere nacional [0.. 1]|nchar [1]|  
|caractere nacional [2.. 255]|nchar [*]|  
|caractere nacional|nchar [1]|  
|variação de caractere nacional|nvarchar [1]|  
|variação de caractere nacional [0.. 1]|nvarchar [1]|  
|variação de caractere nacional [2.. 4000]|nvarchar [*]|  
|variação de caractere nacional [4001.. *]|nvarchar(max)|  
|caractere nacional [0.. 1]|nchar [1]|  
|caractere nacional [2.. 255]|nchar [*]|  
|varchar nacional|nvarchar [1]|  
|varchar nacional [0.. 1]|nvarchar [1]|  
|varchar [2.. 4000] nacional|nvarchar [*]|  
|varchar [4001.. *] nacional|nvarchar(max)|  
|NCHAR|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0.. 1]|nvarchar [1]|  
|nchar varchar [2.. 4000]|nvarchar [*]|  
|nchar varchar [4001.. *]|nvarchar(max)|  
|nchar [0.. 1]|nchar [1]|  
|nchar [2.. 255]|nchar [*]|  
|numeric|numeric|  
|numeric [*.. 65]|numeric [*] [0]|  
|numeric [*.. 65] [ \* .. máximo|numeric [*] [ \* ]|  
|NVARCHAR|nvarchar [1]|  
|nvarchar [0.. 1]|nvarchar [1]|  
|nvarchar [2.. 4000]|nvarchar [*]|  
|nvarchar [4001.. *]|nvarchar(max)|  
|real|float [53]|  
|real [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|serial|BIGINT|  
|SMALLINT|SMALLINT|  
|smallint [*.. 255]|SMALLINT|  
|text|nvarchar(max)|  
|texto [0.. 1]|nvarchar [1]|  
|texto [2.. 4000]|nvarchar [*]|  
|texto [4001.. *]|nvarchar(max)|  
|time|time|  
|timestamp|DATETIME|  
|tinyblob|varbinary [255]|  
|TINYINT|SMALLINT|  
|tinyint [*.. 255]|SMALLINT|  
|tinytext|nvarchar [255]|  
|bigint não assinado|BIGINT|  
|bigint não assinado [*.. 255]|BIGINT|  
|Não assinado Dec|decimal|  
|Não assinado Dec [*.. 65]|Decimal [*] [0]|  
|Não assinado Dec [*.. 65] [ \* .. máximo|Decimal [*] [ \* ]|  
|Decimal sem sinal|decimal|  
|Decimal sem sinal [*.. 65]|Decimal [*] [0]|  
|Decimal sem sinal [*.. 65] [ \* .. máximo|Decimal [*] [ \* ]|  
|duplo não assinado|float [53]|  
|precisão dupla não assinada|float [53]|  
|precisão dupla não assinada [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|duplo não assinado [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|Não assinado corrigido|numeric|  
|Não assinado fixo [*.. 65] [ \* .. máximo|numeric [*] [ \* ]|  
|float não assinado|float [24]|  
|float não assinado [*.. 255] [ \* .. máximo|numeric [*] [ \* ]|  
|float não assinado [*.. 53]|float [53]|  
|unsigned int|BIGINT|  
|int não assinado [*.. 255]|BIGINT|  
|inteiro sem sinal|BIGINT|  
|inteiro sem sinal [*.. 255]|BIGINT|  
|MEDIUMINT não assinado|INT|  
|MEDIUMINT não assinado [*.. 255]|INT|  
|numérico não assinado|numeric|  
|numérico não assinado [*.. 65]|numeric [*] [0]|  
|numérico não assinado [*.. 65] [ \* .. máximo|numeric [*] [ \* ]|  
|real não assinado|float [53]|  
|real não assinado [*.. 255 [[ \* .. máximo|numeric [*] [ \* ]|  
|smallint não assinado|INT|  
|smallint não assinado [*.. 255]|INT|  
|tinyint não assinado|TINYINT|  
|tinyint não assinado [*.. 255]|TINYINT|  
|varbinary [0.. 1]|varbinary [1]|  
|varbinary [2.. 8000]|varbinary [*]|  
|varbinary [8001.. *]|varbinary(max)|  
|varchar [0.. 1]|nvarchar [1]|  
|varchar [2.. 4000]|nvarchar [*]|  
|varchar [4001.. *]|nvarchar(max)|  
|year|SMALLINT|  
|ano [2.. 2]|SMALLINT|  
|ano [4.. 4]|SMALLINT|  
  
##### <a name="add"></a>Adicionar  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
##### <a name="edit"></a>Editar  
Clique para editar um tipo de dados na lista mapeamento.  
  
##### <a name="remove"></a>Remover  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
##### <a name="reset-to-default"></a>Restaurar Padrões  
Clique para redefinir todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
