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
manager: craigg
ms.openlocfilehash: e0a11a0b49589c3763b5af67623c9e819038c217
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713244"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>Configurações do projeto (mapeamento de tipo) (MySQLToSQL)
As configurações de mapeamento de tipo de projeto permitem que você definir mapeamentos de tipo padrão para o projeto do SSMA.  

Mapeamento de tipo está disponível nas caixas de diálogo Configurações do projeto e configurações de projeto padrão:  
  
-   Use a caixa de diálogo de configurações do projeto para definir opções de configuração para o projeto atual. Para acessar as configurações de mapeamento de tipo, no menu Ferramentas, selecione configurações do projeto e, em seguida, no painel esquerdo, clique em mapeamento de tipo.  
  
-   Use a caixa de diálogo de configurações de projeto padrão para definir opções de configuração para todos os projetos. Para acessar o mapeamento de tipo de configurações, no menu Ferramentas, selecione configurações padrão do projeto, tipo de projeto de migração de select para as quais configurações são necessárias para ser exibida / alterado de **versão de destino de migração** lista suspensa e, em seguida, clique em tipo Mapeamento no painel esquerdo.  
  
## <a name="options"></a>Opções  
  
##### <a name="source-type"></a>Tipo de Origem  
É o tipo de dados MySQL, que deve ser mapeado para o tipo de dados do banco de dados de destino.  
  
##### <a name="target-type"></a>Tipo de destino  
Digite os dados do banco de dados de destino para o tipo de dados MySQL especificado.  
  
##### <a name="add"></a>Adicionar  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
##### <a name="edit"></a>Editar  
Clique para editar o tipo de dados selecionado na lista de mapeamento.  
  
##### <a name="remove"></a>Remover  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
##### <a name="reset-to-default"></a>Restaurar Padrões  
Clique para redefinir a lista de mapeamento de tipo para os padrões do SSMA.  
  
## <a name="type-mappings"></a>Mapeamentos de tipo  
A tabela a seguir mostra o mapeamento padrão entre os tipos de dados de origem e destino  
  
|||  
|-|-|  
|**Tipo de dados MySQL**|**Tipo de dados do SQL Server**|  
|BIGINT|BIGINT|  
|bigint [*... 255]|BIGINT|  
|BINARY|binário [1]|  
|binário [de 0 a 1]|binário [1]|  
|binário [2..255]|binary[*]|  
|bit|binário [1]|  
|bit [0..8]|binário [1]|  
|bit [17..24]|binário [3]|  
|bit [25..32]|binary[4]|  
|bit [33..40]|binário [5]|  
|bit [41..48]|binary[6]|  
|bit [49..56]|binary[7]|  
|bit [57..64]|binário [8]|  
|bit [9..16]|binary[2]|  
|blob|varbinary(max)|  
|blob [de 0 a 1]|varbinary[1]|  
|blob[2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|booleano|bit|  
|char|nchar [1]|  
|bytes de char|binário [1]|  
|bytes de char [de 0 a 1]|binário [1]|  
|bytes de char [2..255]|binary[*]|  
|char [entre 0 e 1]|nchar [1]|  
|char [2..255]|nchar [*]|  
|character|nchar [1]|  
|caractere variando [de 0 a 1]|nvarchar [1]|  
|caractere variados [2..255]|NVARCHAR|  
|caractere [de 0 a 1]|nchar [1]|  
|caracteres [2..255]|nchar [*]|  
|Data|Data|  
|DATETIME|datetime2[0]|  
|dec|Decimal|  
|DEC [*... 65]|decimal[*][0]|  
|DEC [*... 65] [\*... 30]|decimal[*][\*]|  
|Decimal|Decimal|  
|decimal [*... 65]|decimal[*][0]|  
|decimal [*... 65] [\*... 30]|decimal[*][\*]|  
|double|float [53]|  
|precisão dupla|float [53]|  
|precisão dupla [*... 255] [\*... 30]|numeric[*][\*]|  
|Double [*... 255] [\*... 30]|numeric[*][\*]|  
|corrigido|NUMERIC|  
|corrigido [*... 65] [\*... 30]|numeric[*][\*]|  
|FLOAT|float[24]|  
|float [*... 255] [\*... 30]|numeric[*][\*]|  
|float [*... 53]|float [53]|  
|INT|INT|  
|int [*... 255]|INT|  
|inteiro|INT|  
|inteiro [*... 255]|INT|  
|longblob|varbinary(max)|  
|longtext|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|INT|  
|mediumint [*... 255]|INT|  
|mediumtext|nvarchar(max)|  
|char nacional|nchar [1]|  
|char nacional [de 0 a 1]|nchar [1]|  
|National char [2..255]|nchar [*]|  
|caracteres nacionais|nchar [1]|  
|a variável de caracteres nacionais|nvarchar [1]|  
|caractere nacional, variando [de 0 a 1]|nvarchar [1]|  
|caractere nacional variados [2..4000]|nvarchar [*]|  
|a variável de caractere nacional [4001... *]|nvarchar(max)|  
|caractere nacional [de 0 a 1]|nchar [1]|  
|caractere nacional [2..255]|nchar [*]|  
|varchar nacional|nvarchar [1]|  
|varchar nacional [de 0 a 1]|nvarchar [1]|  
|varchar nacional [2..4000]|nvarchar [*]|  
|varchar nacional [4001... *]|nvarchar(max)|  
|NCHAR|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [de 0 a 1]|nvarchar [1]|  
|nchar varchar [2..4000]|nvarchar [*]|  
|nchar varchar [4001... *]|nvarchar(max)|  
|nchar [de 0 a 1]|nchar [1]|  
|nchar [2..255]|nchar [*]|  
|NUMERIC|NUMERIC|  
|numérico [*... 65]|numeric[*][0]|  
|numérico [*... 65] [\*... 30]|numeric[*][\*]|  
|NVARCHAR|nvarchar [1]|  
|nvarchar [entre 0 e 1]|nvarchar [1]|  
|nvarchar [2..4000]|nvarchar [*]|  
|nvarchar [4001... *]|nvarchar(max)|  
|REAL|float [53]|  
|real [*... 255] [\*... 30]|numeric[*][\*]|  
|serial|BIGINT|  
|SMALLINT|SMALLINT|  
|smallint [*... 255]|SMALLINT|  
|text|nvarchar(max)|  
|texto [de 0 a 1]|nvarchar [1]|  
|text[2..4000]|nvarchar [*]|  
|texto [4001... *]|nvarchar(max)|  
|time|time|  
|timestamp|DATETIME|  
|tinyblob|varbinary[255]|  
|TINYINT|SMALLINT|  
|tinyint[*..255]|SMALLINT|  
|tinytext|nvarchar [255]|  
|bigint sem sinal|BIGINT|  
|bigint sem sinal [*... 255]|BIGINT|  
|dec sem sinal|Decimal|  
|sem sinal dec [*... 65]|decimal[*][0]|  
|sem sinal dec [*... 65] [\*... 30]|decimal[*][\*]|  
|decimal sem sinal|Decimal|  
|decimal sem assinatura [*... 65]|decimal[*][0]|  
|decimal sem assinatura [*... 65] [\*... 30]|decimal[*][\*]|  
|dupla sem sinal|float [53]|  
|sem sinal de precisão dupla|float [53]|  
|não assinado de precisão dupla [*... 255] [\*... 30]|numeric[*][\*]|  
|não assinado double [*... 255] [\*... 30]|numeric[*][\*]|  
|não assinado fixa|NUMERIC|  
|não assinado fixa [*... 65] [\*... 30]|numeric[*][\*]|  
|float não assinado|float[24]|  
|sem sinal de float [*... 255] [\*... 30]|numeric[*][\*]|  
|sem sinal de float [*... 53]|float [53]|  
|int sem sinal|BIGINT|  
|int sem sinal [*... 255]|BIGINT|  
|inteiro sem sinal|BIGINT|  
|inteiro sem sinal [*... 255]|BIGINT|  
|mediumint sem sinal|INT|  
|sem sinal mediumint [*... 255]|INT|  
|numérico sem sinal|NUMERIC|  
|sem sinal numérico [*... 65]|numeric[*][0]|  
|sem sinal numérico [*... 65] [\*... 30]|numeric[*][\*]|  
|sem sinal real|float [53]|  
|sem o sinal real [*... 255 [[\*... 30]|numeric[*][\*]|  
|smallint não assinado|INT|  
|smallint não assinado [*... 255]|INT|  
|tinyint sem sinal|TINYINT|  
|tinyint não assinado [*... 255]|TINYINT|  
|varbinary [entre 0 e 1]|varbinary[1]|  
|varbinary [2..8000]|varbinary[*]|  
|varbinary [8001... *]|varbinary(max)|  
|varchar [de 0 a 1]|nvarchar [1]|  
|varchar [2..4000]|nvarchar [*]|  
|varchar [4001... *]|nvarchar(max)|  
|year|SMALLINT|  
|ano [2..2]|SMALLINT|  
|ano [4..4]|SMALLINT|  
  
##### <a name="add"></a>Adicionar  
Clique para adicionar um tipo de dados à lista de mapeamento.  
  
##### <a name="edit"></a>Editar  
Clique para editar um tipo de dados na lista de mapeamento.  
  
##### <a name="remove"></a>Remover  
Clique para remover o mapeamento de tipo de dados selecionado da lista de mapeamento.  
  
##### <a name="reset-to-default"></a>Restaurar Padrões  
Clique para redefinir todos os mapeamentos de tipo de dados para os padrões do SSMA.  
  
