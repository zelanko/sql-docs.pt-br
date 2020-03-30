---
title: Suporte a tipo de dados do Microsoft Connector para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c28efd8106056ea900fef0cd57791837cf79e21a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "69553232"
---
# <a name="microsoft-connector-for-oracle-data-type-support"></a>Suporte a tipo de dados do Microsoft Connector para Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Os componentes SSIS para Oracle não dão suporte para todos os tipos de dados do Oracle. As colunas com tipos de dados não compatíveis exibirão um alerta ao criar pacotes no SSDT e serão excluídos das colunas de mapeamento. Os dados não poderão ser carregados em uma coluna com um tipo de dado não compatível.

## <a name="data-type-mapping"></a>Mapeamento de tipo de dados

A tabela a seguir mostra os tipos de dados do banco de dados do Oracle e o mapeamento padrão para os tipos de dados do SSIS. Ela também mostra os tipos de dados não compatíveis do Oracle.

|Tipo de dados de banco de dados Oracle|Tipo de dados SSIS|Comentários|
|:-|:-|:-|
|VARCHAR2|DT_STR||
|NVARCHAR2|DT_WSTR||
|CHAR|DT_STR||
|NUMBER|DT_R8|Isso pode ser alterado para DT_NUMERIC com escala e precisão específicas. A escala e a precisão são definidas pelo usuário conforme a necessidade. A saída será a coluna de dados como um número com escala e precisão fixos.|
|NUMBER(P, S)| Quando a escala for 0, de acordo com a precisão (P) <li> DT_I1 <Li> DT_I2 <Li> DT_I4 <Li> DT_NUMBERIC(P,0)||
||DT_NUMERIC(P,S)||
|DATE|DT_DBTIMESTAMP||
|<li>timestamp <li>TIMESTAMP WITH TIME ZONE <li>INTERVAL YEAR TO MONTH <li>INTERVAL DAY TO SECOND <li>TIMESTAMP WITH LOCAL TIME ZONE|DT_STR||
|RAW|DT_BYTES||
|CLOB|DT_TEXT|Os tipos de dados CLOB, NCLOB e BLOB são compatíveis apenas no modo matriz, não no modo de Carregamento Rápido.|
|NCLOB|DT_NTEXT||
|BLOB|DT_IMAGE||
|UROWID|Sem suporte||
|REF|Sem suporte||
|BFILE|Sem suporte||
|LONG|Sem suporte||
|LONG RAW|Sem suporte||
|ROWID|Sem suporte||
|Tipo definido pelo usuário (tipo de objeto, VARRAY, Tabela Aninhada)|Sem suporte||

## <a name="next-steps"></a>Próximas etapas

- Configurar o [Gerenciador de Conexões do Oracle](oracle-connection-manager.md).
- Configurar a [Origem do Oracle](oracle-source.md).
- Configurar o [Destino Oracle](oracle-destination.md).
- Caso tenha dúvidas, visite a [TechCommunity](https://aka.ms/AA5u35j).
