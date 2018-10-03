---
title: Comando INDEX | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0af3a454963474df483c56e5afddaede77b29dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721064"
---
# <a name="index-command"></a>Comando INDEX
Cria um arquivo de índice para exibir e acessar os registros da tabela em uma ordem lógica.  
  
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
 Especifica uma expressão de índice que pode incluir o nome de um campo ou campos da tabela atual. Uma chave de índice com base em expressão do índice é criada no arquivo de índice para cada registro na tabela. Do Visual FoxPro usa essas chaves para exibir e acessar os registros na tabela.  
  
> [!NOTE]  
>  Embora não seja recomendado, *eExpression* também pode ser uma variável de memória, um elemento de matriz, ou um campo ou expressão de campo de uma tabela em outra área de trabalho. Campos de memorando não podem ser usados sozinho em expressões de arquivo de índice; eles devem ser combinados com outras expressões de caractere. Se você acessar um índice que contém uma variável ou um campo que não existe ou não pode ser localizado, o Visual FoxPro gera uma mensagem de erro.  
  
 Se você tentar criar um índice com uma chave que varia em tamanho, a chave será preenchida com espaços. Chaves de índice de comprimento variável não são suportadas no Visual FoxPro.  
  
 É possível criar uma chave de índice com comprimento zero. Por exemplo, uma chave de índice zero comprimento é criada quando a expressão de índice é uma subcadeia de caracteres de um campo vazio de memorando. Uma chave de índice zero comprimento gera uma mensagem de erro. Quando o Visual FoxPro cria um índice, ele avalia a campos no primeiro registro na tabela. Se um campo está vazio, pode ser necessário inserir alguns dados temporários no campo no primeiro registro para impedir que uma chave de índice de comprimento 0.  
  
 PARA *IDXFileName*  
 Cria um arquivo de índice. idx. O arquivo de índice é dada a extensão de padrão. idx.  
  
 MARCA *TagName*[OF *CDXFileName*]  
 Cria um arquivo de índice composto. Um arquivo de índice composto é um arquivo de índice único que consiste em qualquer número de marcas separadas (entradas de índice). Cada marca é identificada por seu nome de marca exclusivo. Nomes de marca devem começar com uma letra ou um sublinhado e podem conter qualquer combinação de letras, dígitos ou sublinhados até 10. O número de marcas em um arquivo de índice composto é limitado apenas pela memória disponível e espaço em disco.  
  
 Arquivos de índice composto de múltiplas entradas são sempre compactos. Não é necessário incluir COMPACT ao criar um arquivo de índice composto. Nomes de arquivos de índice composto recebem uma extensão. cdx.  
  
 Dois tipos de arquivos de índice composto podem ser criados: estruturais e nonstructural.  
  
 **Arquivos de índice composto estrutural** você pode criar um arquivo de índice composto estrutural com marca *TagName* excluindo o opcional de *CDXFileName* cláusula. Um arquivo de índice composto estrutural sempre tem o mesmo nome que a tabela base e é aberto automaticamente quando a tabela é aberta.  
  
 **Arquivos de índice composto nonstructural** você pode criar um arquivo de índice composto nonstructural incluindo OF *CDXFileName* após a marca *TagName*. Ao contrário de um arquivo de índice composto estrutural, um arquivo de índice composto nonstructural deve ser aberto explicitamente com a cláusula de índice em uso.  
  
 Se um arquivo de índice composto já foi criado e aberto, emitindo o índice com a marca *TagName* adiciona uma marca para o arquivo de índice composto.  
  
 PARA *lExpression*  
 Especifica uma condição na qual somente os registros que satisfazem a expressão de filtro *lExpression* estão disponíveis para exibição e acesso; as chaves de índice são criadas no arquivo de índice para apenas os registros que correspondem à expressão de filtro.  
  
 Tecnologia do Visual FoxPro Rushmore otimiza um índice... PARA *lExpression* comando se *lExpression* é uma expressão otimizável. Para obter melhor desempenho, use uma expressão otimizável na cláusula FOR.  
  
 COMPACTAR  
 Cria um arquivo. idx compact.  
  
 EM ORDEM CRESCENTE  
 Especifica uma ordem crescente para o arquivo. cdx. Por padrão, as marcas. cdx são criadas em ordem crescente. (Você pode incluir CRESCENTE como um lembrete da ordem do arquivo de índice). Uma tabela pode ser indexada na ordem inversa, incluindo DECRESCENTE.  
  
 EM ORDEM DECRESCENTE  
 Especifica uma ordem decrescente para o arquivo. cdx. Você não pode incluir DECRESCENTE durante a criação de arquivos de índice. idx.  
  
 UNIQUE  
 Especifica que apenas o primeiro registro encontrado com um valor de chave de índice específico está incluído em um arquivo. idx ou marca. cdx. UNIQUE pode ser usado para impedir o acesso ou a exibição de registros duplicados. Todos os registros adicionados com chaves de índice duplicados são excluídos do arquivo de índice. Usando a opção exclusiva de índice é idêntico ao executar SET UNIQUE ON antes de emitir o índice ou a REINDEXAÇÃO.  
  
 Quando um índice exclusivo ou uma marca de índice está ativa e um registro duplicado é alterado de forma que as alterações de sua chave de índice, o índice ou a marca de índice é atualizada. No entanto, o próximo registro duplicado com a chave de índice original não é acessado ou exibido até que você reindexar o arquivo usando a REINDEXAÇÃO.  
  
 CANDIDATO  
 Cria uma marca de índice estruturais do candidato. A palavra-chave de CANDIDATO pode ser incluída somente durante a criação de uma marca de índice estruturais; Caso contrário, o Visual FoxPro gera uma mensagem de erro.  
  
 Uma marca de índice do candidato impede que os valores duplicados no campo ou combinação de campos especificados na expressão do índice *eExpression*. O termo *release candidate* refere-se para o tipo de índice; porque os índices de candidato evitar valores duplicados, eles se qualifica como um candidato a"" para ser um índice primário.  
  
 Do Visual FoxPro gerará um erro se você criar uma marca de índice de candidato para um campo ou uma combinação de campos que já contenha valores duplicados.  
  
 ADITIVO  
 Mantém abre qualquer arquivo de índice aberto anteriormente. Se você omitir a cláusula ADITIVA, quando você cria um arquivo de índice ou de arquivos para uma tabela com índice, todos os arquivos (exceto o índice composto estrutural) índice aberto anteriormente são fechados.  
  
## <a name="remarks"></a>Comentários  
 Registros em uma tabela que tem um arquivo de índice são exibidos e acessados na ordem especificada pela expressão de índice. A ordem física dos registros na tabela não é alterada por um arquivo de índice.  
  
## <a name="index-types"></a>Tipos de índice  
 Do Visual FoxPro permite que você criar dois tipos de arquivos de índice:  
  
-   Composta que contém várias entradas de índice, denominadas marcas de arquivos de índice. cdx  
  
-   arquivos de índice. idx que contém uma entrada de índice  
  
 Você também pode criar um arquivo de índice composto estrutural, que é aberto automaticamente com a tabela.  
  
> [!NOTE]  
>  Como arquivos de índice composto estruturais são abertos automaticamente quando a tabela é aberta, eles são o tipo de índice preferencial.  
  
 Inclua o CD para criar arquivos de índice. idx compact. Arquivos de índice composto são sempre compactos.  
  
## <a name="index-order-and-updating"></a>Ordem de índice e a atualização  
 Somente um índice (o arquivo índice mestre) ou marcação (a marca mestre) controla a ordem na qual a tabela é exibida ou acessada. Alguns comandos (por exemplo, busca) usam o arquivo de índice mestre ou a marca para procurar registros. No entanto, todos os abertos. idx e arquivos de índice. cdx são atualizados conforme as alterações são feitas na tabela.  
  
## <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 Embora uma expressão de índice pode conter uma função definida pelo usuário, você não deve usar funções definidas pelo usuário em uma expressão de índice. Funções definidas pelo usuário em uma expressão de índice aumentam o tempo necessário para criar ou atualizar o índice. Além disso, as atualizações do índice não podem ocorrer quando uma função definida pelo usuário é usada para uma expressão de índice.  
  
 Se você usar uma função definida pelo usuário em uma expressão de índice, do Visual FoxPro deve ser capaz de localizar a função definida pelo usuário. Quando o Visual FoxPro cria um índice, a expressão de índice é salvo no arquivo de índice, mas apenas uma referência para a função definida pelo usuário está incluída na expressão do índice.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE – comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando DELETE TAG](../../odbc/microsoft/delete-tag-command.md)   
 [Comando SET COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [Comando SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
