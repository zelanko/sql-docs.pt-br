---
title: Desempenho da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
author: rothja
ms.author: jroth
ms.openlocfilehash: d478c9da4455b4c343a323ffa33eb742f50be7bb
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212425"
---
# <a name="clr-integration-architecture----performance"></a>Arquitetura de integração de CLR – Desempenho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Este tópico discute algumas das opções de design que aprimoram o desempenho da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integração com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR).  
  
## <a name="the-compilation-process"></a>O processo de compilação  
 Durante a compilação de expressões SQL, quando é encontrada uma referência a uma rotina, é gerado um stub do MSIL ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language). Esse stub inclui código para realizar marshaling dos parâmetros de rotina do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o CLR, invocar a função e retornar o resultado. Este código de "cola" se baseia no tipo de parâmetro e na direção do parâmetro (de entrada, de saída ou de referência).  
  
 O código cola permite otimizações específicas do tipo e assegura a imposição eficiente da semântica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como a nulidade, a restrição de facetas, o tratamento de exceções por valor e padrão. Ao gerar código para os tipos exatos dos argumentos, você evita a coerção de tipos ou custos com a criação de objetos wrapper (o chamado "boxing") além do limite de invocação.  
  
 O stub gerado é então compilado em código nativo e otimizado para a arquitetura de hardware específica na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado, usando os serviços de compilação JIT (just-in-time) do CLR. Os serviços JIT são invocados no nível de método e permitem que o ambiente de hospedagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crie uma única unidade de compilação que se estende pelas execuções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do CLR. Depois que o stub é compilado, o ponteiro de função resultante se torna a implementação em tempo de execução da função. Essa abordagem da geração de código assegura que não haja custos adicionais com a invocação relacionados com a reflexão ou o acesso de metadados em tempo de execução.  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>Transições rápidas entre o SQL Server e o CLR  
 O processo de compilação gera um ponteiro de função que pode ser chamado em tempo de execução a partir do código nativo. No caso de funções definidas pelo usuário com valor escalar, essa invocação de função ocorre por linha. A fim de minimizar o custo da transição entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR, as instruções que contêm qualquer invocação gerenciada têm uma etapa de inicialização para identificar o domínio do aplicativo de destino. Essa etapa de identificação reduz o custo de transição de cada linha.  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Segue um resumo das considerações de desempenho específicas da integração CLR no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Informações mais detalhadas podem ser encontradas em "[usando a integração CLR no SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=50332)" no site do MSDN. Informações gerais sobre o desempenho do código gerenciado podem ser encontradas em "melhorando o[desempenho e a escalabilidade do aplicativo .net](https://go.microsoft.com/fwlink/?LinkId=50333)" no site do MSDN.  
  
### <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 As funções CLR se beneficiam de um caminho de invocação mais rápido que o das funções definidas pelo usuário do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Além disso, o código gerenciado tem uma vantagem de desempenho decisiva sobre o [!INCLUDE[tsql](../../includes/tsql-md.md)] em termos de código de procedimento, computação e manipulação de cadeias de caracteres. As funções CLR que utilizam muitos recursos de computação e que não executam acesso a dados são melhor escritas em código gerenciado. Entretanto, as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] executam o acesso a dados de forma mais eficiente que a integração CLR.  
  
### <a name="user-defined-aggregates"></a>Agregações definidas pelo usuário  
 O código gerenciado pode ter um desempenho significativamente melhor que a agregação baseada em cursor. Em geral, o desempenho do código gerenciado é um pouco mais lento que o das funções de agregação internas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se houver uma função de agregação interna nativa, é recomendável utilizá-la. Nos casos em que não há suporte nativo para a agregação necessária, por motivos de desempenho, considere uma agregação CLR definida pelo usuário como superior a uma implementação baseada em cursor.  
  
### <a name="streaming-table-valued-functions"></a>Funções de streaming com valor de tabela  
 Frequentemente, os aplicativos precisam retornar uma tabela como resultado da invocação de uma função. Exemplos incluem a leitura de dados tabulares de um arquivo como parte de uma operação de importação e a conversão de valores separados por vírgula em uma representação relacional. Normalmente, isso pode ser feito materializando e preenchendo a tabela de resultados antes de ela poder ser consumida pelo chamador. A integração do CLR no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] introduz um novo mecanismo de extensibilidade chamado STVF (função de streaming com valor de tabela). As STVFs gerenciadas têm um desempenho melhor que o de implementações de procedimentos armazenados estendidos comparáveis.  
  
 STVFs são funções gerenciadas que retornam uma interface **IEnumerable** . **IEnumerable** tem métodos para navegar no conjunto de resultados RETORNADO pelo STVF. Quando o STVF é invocado, o **IEnumerable** retornado é conectado diretamente ao plano de consulta. O plano de consulta chama métodos **IEnumerable** quando precisa buscar linhas. Esse modelo de iteração permite que os resultados sejam consumidos imediatamente depois que a primeira linha é gerada, em vez de aguardar até que toda a tabela seja preenchida. Ele também reduz significativamente a memória consumida ao invocar a função.  
  
### <a name="arrays-vs-cursors"></a>Matrizes vs. Cursores  
 Quando os cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] devem atravessar dados que são expressos mais facilmente como uma matriz, é possível usar código gerenciado com ganhos de desempenho significativos.  
  
### <a name="string-data"></a>Dados de cadeia de caracteres  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os dados de caractere, como **varchar**, podem ser do tipo SqlString ou SqlChars em funções gerenciadas. As variáveis SqlString criam uma instância do valor inteiro na memória. As variáveis SqlChars fornecem uma interface de streaming que pode ser usada para obter um melhor desempenho e escalabilidade por não criar uma instância do valor inteiro na memória. Isso se torna especialmente importante no caso de dados LOB (objeto grande). Além disso, os dados do servidor XML podem ser acessados por meio de uma interface de streaming retornada por **SQLXML. CreateReader ()** .  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR vs. Procedimentos armazenados estendidos  
 As APIs Microsoft.SqlServer.Server que permitem que procedimentos gerenciados enviem conjuntos de resultados de volta ao cliente têm um desempenho melhor que as APIs ODS (Open Data Services) usadas por procedimentos armazenados estendidos. Além disso, as APIs System. Data. SqlServer dão suporte a tipos de dados como **XML**, **varchar (max)** , **nvarchar (max)** e **varbinary (max)** , [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]introduzidos no, enquanto as APIs de ODS não foram estendidas para dar suporte ao novo tipos de dados.  
  
 Com o código gerenciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia o uso de recursos como a memória, os threads e a sincronização. Isso se deve ao fato de as APIs gerenciadas que expõem esses recursos serem implementadas sobre o gerenciador de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por outro lado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem nenhuma exibição ou controle sobre o uso de recursos do procedimento armazenado estendido. Por exemplo, se um procedimento armazenado estendido consumir muitos recursos de CPU ou de memória, não há uma forma de detectá-lo ou controlá-lo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Contudo, com o código gerenciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode detectar que um determinado thread não teve resultados por um longo período e então forçar a geração da tarefa, de forma que outros trabalhos possam ser agendados. Consequentemente, o uso do código gerenciado fornece uma escalabilidade e um uso de recursos do sistema melhores.  
  
 O código gerenciado pode incorrer em uma sobrecarga adicional necessária para manter o ambiente de execução e executar verificações de segurança. Isso ocorre, por exemplo, ao executar no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando várias transições do código gerenciado para o código nativo são necessárias (porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa executar uma manutenção adicional em configurações específicas de threads ao passar para o código nativo e voltar). Consequentemente, os procedimentos armazenados estendidos podem ter um desempenho significativamente melhor que o código gerenciado executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nos casos em que há transições frequentes entre o código gerenciado e o código nativo.  
  
> [!NOTE]  
>  É recomendável não desenvolver novos procedimentos armazenados estendidos, pois esse recurso foi preterido.  
  
### <a name="native-serialization-for-user-defined-types"></a>Serialização nativa para tipos definidos pelo usuário  
 Os UDTs (tipos definidos pelo usuário) são criados como um mecanismo de extensibilidade para o sistema de tipo de escalar. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementa um formato de serialização para UDTs chamado **Format. Native**. Durante a compilação, a estrutura do tipo é examinada para gerar MSIL personalizado para esta definição de tipo de particular.  
  
 A serialização nativa é a implementação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A serialização definida pelo usuário invoca um método definido pelo autor do tipo para fazer a serialização. **Formato.** a serialização nativa deve ser usada quando possível para melhor desempenho.  
  
### <a name="normalization-of-comparable-udts"></a>Normalização de UDTs comparáveis  
 As operações relacionais, como a classificação e a comparação de UDTs, funcionam diretamente na representação binária do valor. Isto é realizado armazenando uma representação normalizada (em ordem binária) do estado do UDT no disco.  
  
 A normalização tem duas vantagens: torna a operação de comparação consideravelmente menos cara por evitar a construção da instância de tipo e a sobrecarga de invocação do método, além de criar um domínio binário para o UDT, permitindo a construção de histogramas, índices e histogramas de valores do tipo. Consequentemente, os UDTs normalizados têm um perfil de desempenho muito semelhante ao dos tipos internos nativos para operações que não envolvem a invocação do método.  
  
### <a name="scalable-memory-usage"></a>Uso da memória escalonável  
 Para que coleta de lixo gerenciada seja executada e bem-escalada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], evite uma única alocação grande. As alocações com mais de 88 quilobytes (KB) serão colocadas no heap de objetos grandes, que fará o desempenho e a escala da coleta de lixo serem muito piores que no caso de várias alocações menores. Por exemplo, se você precisar alocar uma matriz multidimensional grande, é melhor alocar uma matriz denteada (dispersa).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos definidos pelo usuário do CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
