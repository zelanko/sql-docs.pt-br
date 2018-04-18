---
title: Desempenho da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
caps.latest.revision: 43
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 285df1ab327617437fa9edf32f21b84b2499e0ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="clr-integration-architecture----performance"></a>Arquitetura de integração de CLR - desempenho
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico discute algumas das opções de design que aprimoram o desempenho de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integração com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] runtime de linguagem comum (CLR) do .NET Framework.  
  
## <a name="the-compilation-process"></a>O processo de compilação  
 Durante a compilação de expressões SQL, quando é encontrada uma referência a uma rotina, é gerado um stub do MSIL ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language). Esse stub inclui código para realizar marshaling dos parâmetros de rotina do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o CLR, invocar a função e retornar o resultado. Este código de "cola" se baseia no tipo de parâmetro e na direção do parâmetro (de entrada, de saída ou de referência).  
  
 O código cola permite otimizações específicas do tipo e assegura a imposição eficiente da semântica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como a nulidade, a restrição de facetas, o tratamento de exceções por valor e padrão. Ao gerar código para os tipos exatos dos argumentos, você evita a coerção de tipos ou custos com a criação de objetos wrapper (o chamado "boxing") além do limite de invocação.  
  
 O stub gerado é então compilado em código nativo e otimizado para a arquitetura de hardware específica na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado, usando os serviços de compilação JIT (just-in-time) do CLR. Os serviços JIT são invocados no nível de método e permitem que o ambiente de hospedagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crie uma única unidade de compilação que se estende pelas execuções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do CLR. Depois que o stub é compilado, o ponteiro de função resultante se torna a implementação em tempo de execução da função. Essa abordagem da geração de código assegura que não haja custos adicionais com a invocação relacionados com a reflexão ou o acesso de metadados em tempo de execução.  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>Transições rápidas entre o SQL Server e o CLR  
 O processo de compilação gera um ponteiro de função que pode ser chamado em tempo de execução a partir do código nativo. No caso de funções definidas pelo usuário com valor escalar, essa invocação de função ocorre por linha. A fim de minimizar o custo da transição entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR, as instruções que contêm qualquer invocação gerenciada têm uma etapa de inicialização para identificar o domínio do aplicativo de destino. Essa etapa de identificação reduz o custo de transição de cada linha.  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Segue um resumo das considerações de desempenho específicas da integração CLR no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Informações mais detalhadas podem ser encontradas em "[usando a integração de CLR no SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=50332)" no site do MSDN. Informações gerais sobre o desempenho de código gerenciado podem ser encontradas em "[melhorando o desempenho de aplicativos .NET e a escalabilidade](http://go.microsoft.com/fwlink/?LinkId=50333)" no site do MSDN.  
  
### <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 As funções CLR se beneficiam de um caminho de invocação mais rápido que o das funções definidas pelo usuário do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Além disso, o código gerenciado tem uma vantagem de desempenho decisiva sobre o [!INCLUDE[tsql](../../includes/tsql-md.md)] em termos de código de procedimento, computação e manipulação de cadeias de caracteres. As funções CLR que utilizam muitos recursos de computação e que não executam acesso a dados são melhor escritas em código gerenciado. Entretanto, as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] executam o acesso a dados de forma mais eficiente que a integração CLR.  
  
### <a name="user-defined-aggregates"></a>Agregações definidas pelo usuário  
 O código gerenciado pode ter um desempenho significativamente melhor que a agregação baseada em cursor. Em geral, o desempenho do código gerenciado é um pouco mais lento que o das funções de agregação internas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se houver uma função de agregação interna nativa, é recomendável utilizá-la. Nos casos em que não há suporte nativo para a agregação necessária, por motivos de desempenho, considere uma agregação CLR definida pelo usuário como superior a uma implementação baseada em cursor.  
  
### <a name="streaming-table-valued-functions"></a>Funções de streaming com valor de tabela  
 Frequentemente, os aplicativos precisam retornar uma tabela como resultado da invocação de uma função. Exemplos incluem a leitura de dados tabulares de um arquivo como parte de uma operação de importação e a conversão de valores separados por vírgula em uma representação relacional. Normalmente, isso pode ser feito materializando e preenchendo a tabela de resultados antes de ela poder ser consumida pelo chamador. A integração do CLR no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] introduz um novo mecanismo de extensibilidade chamado STVF (função de streaming com valor de tabela). As STVFs gerenciadas têm um desempenho melhor que o de implementações de procedimentos armazenados estendidos comparáveis.  
  
 As STVFs são funções gerenciadas que retornam um **IEnumerable** interface. **IEnumerable** tem métodos para navegar pelo conjunto de resultados retornado pela STVF. Quando a STVF é invocada, retornado **IEnumerable** está conectado diretamente ao plano de consulta. O plano de consulta chamará **IEnumerable** métodos quando ele precisa buscar linhas. Esse modelo de iteração permite que os resultados sejam consumidos imediatamente depois que a primeira linha é gerada, em vez de aguardar até que toda a tabela seja preenchida. Ele também reduz significativamente a memória consumida ao invocar a função.  
  
### <a name="arrays-vs-cursors"></a>Matrizes vs. Cursores  
 Quando os cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] devem atravessar dados que são expressos mais facilmente como uma matriz, é possível usar código gerenciado com ganhos de desempenho significativos.  
  
### <a name="string-data"></a>Dados de cadeia de caracteres  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados de caractere, como **varchar**, pode ser do tipo SqlString ou SqlChars em funções gerenciadas. As variáveis SqlString criam uma instância do valor inteiro na memória. As variáveis SqlChars fornecem uma interface de streaming que pode ser usada para obter um melhor desempenho e escalabilidade por não criar uma instância do valor inteiro na memória. Isso se torna especialmente importante no caso de dados LOB (objeto grande). Além disso, os dados XML do servidor pode ser acessado por meio de uma interface de streaming retornada por **SqlXml.CreateReader()**.  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR vs. Procedimentos armazenados estendidos  
 As APIs Microsoft.SqlServer.Server que permitem que procedimentos gerenciados enviem conjuntos de resultados de volta ao cliente têm um desempenho melhor que as APIs ODS (Open Data Services) usadas por procedimentos armazenados estendidos. Além disso, os APIs System.Data.SqlServer suporte a tipos de dados como **xml**, **varchar (max)**, **nvarchar (max)**, e **varbinary (max)**, apresentada no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], enquanto as APIs ODS não foram estendidas para oferecer suporte a novos tipos de dados.  
  
 Com o código gerenciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia o uso de recursos como a memória, os threads e a sincronização. Isso se deve ao fato de as APIs gerenciadas que expõem esses recursos serem implementadas sobre o gerenciador de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por outro lado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem nenhuma exibição ou controle sobre o uso de recursos do procedimento armazenado estendido. Por exemplo, se um procedimento armazenado estendido consumir muitos recursos de CPU ou de memória, não há uma forma de detectá-lo ou controlá-lo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Contudo, com o código gerenciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode detectar que um determinado thread não teve resultados por um longo período e então forçar a geração da tarefa, de forma que outros trabalhos possam ser agendados. Consequentemente, o uso do código gerenciado fornece uma escalabilidade e um uso de recursos do sistema melhores.  
  
 O código gerenciado pode incorrer em uma sobrecarga adicional necessária para manter o ambiente de execução e executar verificações de segurança. Isso ocorre, por exemplo, ao executar no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando várias transições do código gerenciado para o código nativo são necessárias (porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa executar uma manutenção adicional em configurações específicas de threads ao passar para o código nativo e voltar). Consequentemente, os procedimentos armazenados estendidos podem ter um desempenho significativamente melhor que o código gerenciado executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nos casos em que há transições frequentes entre o código gerenciado e o código nativo.  
  
> [!NOTE]  
>  É recomendável não desenvolver novos procedimentos armazenados estendidos, pois esse recurso foi preterido.  
  
### <a name="native-serialization-for-user-defined-types"></a>Serialização nativa para tipos definidos pelo usuário  
 Os UDTs (tipos definidos pelo usuário) são criados como um mecanismo de extensibilidade para o sistema de tipo de escalar. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa um formato de serialização para UDTs chamado **Format.Native**. Durante a compilação, a estrutura do tipo é examinada para gerar MSIL personalizado para esta definição de tipo de particular.  
  
 A serialização nativa é a implementação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A serialização definida pelo usuário invoca um método definido pelo autor do tipo para fazer a serialização. **Format.Native** serialização deve ser usada quando possível para melhor desempenho.  
  
### <a name="normalization-of-comparable-udts"></a>Normalização de UDTs comparáveis  
 As operações relacionais, como a classificação e a comparação de UDTs, funcionam diretamente na representação binária do valor. Isto é realizado armazenando uma representação normalizada (em ordem binária) do estado do UDT no disco.  
  
 A normalização tem duas vantagens: torna a operação de comparação consideravelmente menos cara por evitar a construção da instância de tipo e a sobrecarga de invocação do método, além de criar um domínio binário para o UDT, permitindo a construção de histogramas, índices e histogramas de valores do tipo. Consequentemente, os UDTs normalizados têm um perfil de desempenho muito semelhante ao dos tipos internos nativos para operações que não envolvem a invocação do método.  
  
### <a name="scalable-memory-usage"></a>Uso da memória escalonável  
 Para que coleta de lixo gerenciada seja executada e bem-escalada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], evite uma única alocação grande. As alocações com mais de 88 quilobytes (KB) serão colocadas no heap de objetos grandes, que fará o desempenho e a escala da coleta de lixo serem muito piores que no caso de várias alocações menores. Por exemplo, se você precisar alocar uma matriz multidimensional grande, é melhor alocar uma matriz denteada (dispersa).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
