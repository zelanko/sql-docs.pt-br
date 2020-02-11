---
title: Conectar-se a um arquivo simples (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connflatfile.f1
ms.assetid: a365991e-eded-4cd8-89c0-0daf6d658d15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6eeb17662c0cac290a7a455d0925cd05560e5e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087357"
---
# <a name="connect-to-a-flat-file-ssas"></a>Conectar a um arquivo simples (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a se conectar a um arquivo simples (.txt), um arquivo separado por tabulações (.tab) ou um arquivo separado por vírgulas (.csv). Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar um arquivo simples, você deve ter o provedor ACE instalado no computador. Para obter mais informações, consulte [Fontes de dados com suporte &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um arquivo nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do arquivo selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Caminho do arquivo**  
 Especifique o caminho completo para o arquivo.  
  
 **Procurar**  
 Navegue até um local onde um arquivo está disponível.  
  
 **Separador de coluna**  
 Selecione de uma lista de separadores de colunas disponíveis. Escolha um separador com pouca probabilidade de ocorrer no texto.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|Tabulação (t)|As colunas são separadas por uma tabulação (t).|  
|Vírgula (,)|As colunas são separadas por uma vírgula (,).|  
|Ponto-e-vírgula (;)|As colunas são separadas por um ponto-e-vírgula (;).|  
|Espaço ( )|As colunas são separadas por um espaço ( ).|  
|Dois-pontos (:)|As colunas são separadas por dois-pontos (:).|  
|Barra vertical (&#124;)|As colunas são separadas por uma barra vertical (&#124;).|  
  
 **Avançado**  
 Especifique a codificação e as opções de localidade para o arquivo simples.  
  
 **Usar primeira linha como cabeçalhos de coluna**  
 Especifique se deseja usar a primeira linha de dados como o cabeçalho de coluna da tabela de destino.  
  
 **Visualização de dados**  
 Visualize os dados na tabela selecionada e use as opções a seguir para modificar a importação de dados.  
  
> [!NOTE]  
>  São exibidas somente as primeiras 50 linhas do arquivo nesta visualização.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Caixa de seleção no cabeçalho da coluna**|Marque a caixa de seleção para incluir a coluna na importação de dados. Desmarque a caixa de seleção para remover a coluna da importação de dados.|  
|**Botão de seta para baixo no cabeçalho da coluna**|Classifique e filtre dados na coluna.|  
  
 **Limpar Filtros de Linha**  
 Remova todos os filtros aplicados aos dados nas colunas.  
  
  
