---
title: Comando de índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300026"
---
# <a name="index-command"></a>Comando INDEX
Cria um arquivo de índice para exibir e acessar os registros de tabela em uma ordem lógica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *eExpression*  
 Especifica uma expressão de índice que pode incluir o nome de um campo ou campos da tabela atual. Uma chave de índice baseada na expressão de índice é criada no arquivo de índice para cada registro na tabela. O Visual FoxPro usa essas chaves para exibir e acessar registros na tabela.  
  
> [!NOTE]  
>  Embora não seja recomendado, *eExpression* também pode ser uma variável de memória, um elemento de matriz ou uma expressão de campo ou campo de uma tabela em outra área de trabalho. Campos de memorando não podem ser usados sozinhas em expressões de arquivo de índice; Eles devem ser combinados com outras expressões de caractere. Se você acessar um índice que contém uma variável ou campo que não existe mais ou não pode ser localizado, o Visual FoxPro gerará uma mensagem de erro.  
  
 Se você tentar criar um índice com uma chave que varie de comprimento, a chave será preenchida com espaços. Não há suporte para chaves de índice de comprimento variável no Visual FoxPro.  
  
 É possível criar uma chave de índice com comprimento zero. Por exemplo, uma chave de índice de comprimento zero é criada quando a expressão de índice é uma subcadeia de caracteres de um campo de memorando vazio. Uma chave de índice de comprimento zero gera uma mensagem de erro. Quando o Visual FoxPro cria um índice, ele avalia os campos no primeiro registro da tabela. Se um campo estiver vazio, talvez seja necessário inserir alguns dados temporários no campo no primeiro registro para evitar uma chave de índice de comprimento 0.  
  
 PARA *IDXFileName*  
 Cria um arquivo de índice. idx. O arquivo de índice recebe a extensão padrão. idx.  
  
 MARCAR *TagName*[of *CDXFileName*]  
 Cria um arquivo de índice composto. Um arquivo de índice composto é um único arquivo de índice que consiste em qualquer número de marcas separadas (entradas de índice). Cada marca é identificada por seu nome de marca exclusivo. Os nomes de marca devem começar com uma letra ou um sublinhado e podem consistir em qualquer combinação de até 10 letras, dígitos ou sublinhados. O número de marcas em um arquivo de índice composto é limitado apenas pela memória disponível e pelo espaço em disco.  
  
 Arquivos de índice composto de várias entradas são sempre compactados. Não é necessário incluir o COMPACT ao criar um arquivo de índice composto. Os nomes dos arquivos de índice compostos recebem uma extensão. CDX.  
  
 Dois tipos de arquivos de índice compostos podem ser criados: estrutural e não estrutural.  
  
 **Arquivos de índice composto estrutural** Você pode criar um arquivo de índice composto estrutural com a marca *TagName* , excluindo o opcional da cláusula *CDXFileName* . Um arquivo de índice composto estrutural sempre tem o mesmo nome base que a tabela e é aberto automaticamente quando a tabela é aberta.  
  
 **Arquivos de índice composto não estrutural** Você pode criar um arquivo de índice composto não estrutural incluindo *CDXFileName* após a marca *TagName*. Ao contrário de um arquivo de índice composto estrutural, um arquivo de índice composto não estrutural deve ser aberto explicitamente com a cláusula INDEX em uso.  
  
 Se um arquivo de índice composto já tiver sido criado e aberto, o índice emissora com a marca *TagName* adicionará uma marca ao arquivo de índice composto.  
  
 PARA *lExpression*  
 Especifica uma condição na qual somente os registros que atendem à expressão de filtro *lExpression* estão disponíveis para exibição e acesso; as chaves de índice são criadas no arquivo de índice apenas para os registros que correspondem à expressão de filtro.  
  
 A tecnologia Rushmore do Visual FoxPro otimiza um índice... PARA o comando *lExpression* se *lExpression* for uma expressão otimizável. Para obter o melhor desempenho, use uma expressão otimizável na cláusula FOR.  
  
 COMPACTÁ  
 Cria um arquivo Compact. idx.  
  
 CRESCENTE  
 Especifica uma ordem crescente para o arquivo. CDX. Por padrão, as marcas. CDX são criadas em ordem crescente. (Você pode incluir em ordem crescente como um lembrete da ordem do arquivo de índice.) Uma tabela pode ser indexada em ordem inversa, incluindo decrescente.  
  
 DECRESCENTE  
 Especifica uma ordem decrescente para o arquivo. CDX. Não é possível incluir decrescente ao criar arquivos de índice. idx.  
  
 UNIQUE  
 Especifica que somente o primeiro registro encontrado com um valor de chave de índice específico está incluído em um arquivo. idx ou em uma marca. CDX. EXCLUSIVO pode ser usado para impedir a exibição ou o acesso a registros duplicados. Todos os registros adicionados com chaves de índice duplicadas são excluídos do arquivo de índice. O uso da opção UNIQUE de INDEX é idêntico à execução de SET UNIQUE ON antes de emitir o índice ou reindexar.  
  
 Quando uma marca de índice ou índice exclusivo está ativa e um registro duplicado é alterado de uma maneira que altera sua chave de índice, a marca índice ou índice é atualizada. No entanto, o próximo registro duplicado com a chave de índice original não pode ser acessado ou exibido até que você reindexe o arquivo usando REINDEX.  
  
 CANDIDATE  
 Cria uma marca de índice estrutural candidato. A palavra-chave candidata pode ser incluída somente ao criar uma marca de índice estrutural; caso contrário, o Visual FoxPro gerará uma mensagem de erro.  
  
 Uma marca de índice candidato impede valores duplicados no campo ou na combinação de campos especificados na expressão de índice *eExpression*. O termo *candidato* refere-se ao tipo de índice; como os índices candidatos impedem valores duplicados, eles se qualificam como um "candidato" para ser um índice primário.  
  
 O Visual FoxPro gerará um erro se você criar uma marca de índice candidato para um campo ou uma combinação de campos que já contenham valores duplicados.  
  
 CUMULATIVO  
 O continua a abrir todos os arquivos de índice abertos anteriormente. Se você omitir a cláusula aditiva ao criar um arquivo de índice ou arquivos para uma tabela com índice, todos os arquivos de índice abertos anteriormente (exceto o índice composto estrutural) serão fechados.  
  
## <a name="remarks"></a>Comentários  
 Os registros em uma tabela que tem um arquivo de índice são exibidos e acessados na ordem especificada pela expressão de índice. A ordem física dos registros na tabela não é alterada por um arquivo de índice.  
  
## <a name="index-types"></a>Tipos de índice  
 O Visual FoxPro permite criar dois tipos de arquivos de índice:  
  
-   Arquivos de índice. cdx compostos que contêm várias entradas de índice chamadas marcas  
  
-   arquivos de índice. idx contendo uma entrada de índice  
  
 Você também pode criar um arquivo de índice composto estrutural, que é aberto automaticamente com a tabela.  
  
> [!NOTE]  
>  Como os arquivos de índice composto estrutural são abertos automaticamente quando a tabela é aberta, eles são o tipo de índice preferencial.  
  
 Inclua COMPACT para criar arquivos de índice Compact. idx. Os arquivos de índice compostos são sempre compactados.  
  
## <a name="index-order-and-updating"></a>Ordem de índice e atualização  
 Somente um arquivo de índice (o arquivo de índice mestre) ou marca (a marca mestra) controla a ordem na qual a tabela é exibida ou acessada. Determinados comandos (SEEK, por exemplo) usam a marca ou o arquivo de índice mestre para pesquisar registros. No entanto, todos os arquivos de índice Open. idx e. CDX são atualizados conforme são feitas alterações na tabela.  
  
## <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 Embora uma expressão de índice possa conter uma função definida pelo usuário, você não deve usar funções definidas pelo usuário em uma expressão de índice. As funções definidas pelo usuário em uma expressão de índice aumentam o tempo necessário para criar ou atualizar o índice. Além disso, as atualizações de índice podem não ocorrer quando uma função definida pelo usuário é usada para uma expressão de índice.  
  
 Se você usar uma função definida pelo usuário em uma expressão de índice, o Visual FoxPro deverá ser capaz de localizar a função definida pelo usuário. Quando o Visual FoxPro cria um índice, a expressão de índice é salva no arquivo de índice, mas apenas uma referência à função definida pelo usuário é incluída na expressão de índice.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE-comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando excluir marca](../../odbc/microsoft/delete-tag-command.md)   
 [Definir comando COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [Comando SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
