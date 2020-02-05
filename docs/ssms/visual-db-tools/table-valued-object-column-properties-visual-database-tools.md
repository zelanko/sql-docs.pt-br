---
title: Propriedades do Objeto com Valor de Tabela (Coluna)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: d5c82466168714f6a58055e1ed50959602318ef3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242159"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>Propriedades de (coluna) de objeto com valor de tabela (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essas propriedades aparecem quando uma coluna de objeto com valor de tabela é selecionada no painel **Diagrama** do Designer de Consulta e Exibição.  
  
> [!NOTE]  
> As propriedades desse tópico são classificadas por categoria e não em ordem alfabética.  
  
> [!NOTE]  
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** .  
  
**Categoria de identidade**  
Expande para mostrar o **Nome** da propriedade.  
  
**Nome**  
Mostra o nome da coluna selecionada.  
  
**Categoria Designer de Consultas**  
Expande para mostrar as propriedades de **Permitir Nulos**, **Ordenação**, **Tipo de dados**, **Comprimento**, **Precisão**, **Escala**e **Tamanho**.  
  
**Permitir Nulos**  
Mostra se o tipo de dados da coluna permite ou não valores nulos.  
  
**Ordenação**  
Mostra a configuração de ordenação da coluna selecionada. A ordenação pode ser definida na guia Propriedades de coluna do Designer de Tabela.  
  
**Tipo de Dados**  
Mostra o tipo de dados da coluna selecionada.  
  
**Comprimento**  
Mostra o número de caracteres ou dígitos permitidos pelo tipo de dados da coluna selecionada. Essa propriedade só fica disponível para tipos de dados baseados em caractere.  
  
> [!NOTE]  
> Para o tamanho em bytes, consulte a propriedade **Tamanho** abaixo.  
  
**Precisão**  
Mostra o número máximo de dígitos permitido para tipos de dados numéricos. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
**Escala**  
Mostra o número máximo de dígitos que podem aparecer à direita do ponto decimal para tipos de dados numéricos. Esse valor deve ser menor do que ou igual à precisão. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
**Tamanho**  
Mostra o tamanho em bytes permitidos pelo tipo de dados da coluna. Por exemplo, um tipo de dados nchar pode ter um comprimento de 10 (número de caracteres), mas teria um tamanho de 20 para conjuntos de caracteres de Unicode.  
  
