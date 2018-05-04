---
title: Comando índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5d5be9318a701b23dc0f6ceb67b9056c2455c7d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="index-command"></a>Comando de índice
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
 Especifica uma expressão de índice que pode incluir o nome de um ou mais campos da tabela atual. Uma chave de índice com base na expressão de índice é criada no arquivo de índice para cada registro na tabela. Do Visual FoxPro usa essas chaves para exibir e acessar os registros na tabela.  
  
> [!NOTE]  
>  Embora não seja recomendado, *eExpression* também pode ser uma variável de memória, um elemento de matriz, ou um campo ou expressão de campo de uma tabela em outra área de trabalho. Campos de memorando não podem ser usados sozinho em expressões de arquivo de índice; eles devem ser combinados com outras expressões de caractere. Se você acessar um índice que contém uma variável ou um campo que não existe ou não pode ser localizado, Visual FoxPro gera uma mensagem de erro.  
  
 Se você tentar criar um índice com uma chave que variam em comprimento, a chave será preenchida com espaços. Chaves de índice de comprimento variável não são suportadas no Visual FoxPro.  
  
 É possível criar uma chave de índice com comprimento zero. Por exemplo, uma chave de índice zero comprimento é criada quando a expressão de índice é uma subcadeia de caracteres de um campo vazio de memorando. Uma chave de índice zero comprimento gera uma mensagem de erro. Quando o Visual FoxPro cria um índice, ele avalia campos no primeiro registro na tabela. Se um campo está vazio, ele pode ser necessário inserir alguns dados temporários no campo no primeiro registro para impedir que uma chave de índice de comprimento 0.  
  
 PARA *IDXFileName*  
 Cria um arquivo de índice. idx. O arquivo de índice tem a extensão de padrão. idx.  
  
 MARCA *TagName*[OF *CDXFileName*]  
 Cria um arquivo de índice composto. Um arquivo de índice composto é um arquivo de índice único que consiste em qualquer número de marcas separadas (entradas de índice). Cada marca é identificada por seu nome de marca exclusivo. Nomes de marca devem começar com uma letra ou um sublinhado e podem consistir em qualquer combinação de letras, dígitos ou sublinhados até 10. O número de marcas em um arquivo de índice composto é limitado apenas pela memória disponível e espaço em disco.  
  
 Arquivos de índice composto múltiplas entradas são sempre compactos. Não é necessário incluir COMPACT ao criar um arquivo de índice composto. Nomes de arquivos de índice composto terá uma extensão. cdx.  
  
 Podem ser criados dois tipos de arquivos de índice composto: estruturais e nonstructural.  
  
 **Arquivos de índice composto estrutural** você pode criar um arquivo de índice composto estrutural com marca *TagName* excluindo o opcional de *CDXFileName* cláusula. Um arquivo de índice composto estrutural sempre tem o mesmo nome que a tabela base e é aberto automaticamente quando a tabela é aberta.  
  
 **Arquivos de índice composto nonstructural** você pode criar um arquivo de índice composto nonstructural incluindo de *CDXFileName* após a marca *TagName*. Ao contrário de um arquivo de índice composto estrutural, um arquivo de índice composto nonstructural deve ser aberto explicitamente com a cláusula de índice em uso.  
  
 Se um arquivo de índice composto já foi criado e aberto, emitindo o índice com marca *TagName* adiciona uma marca ao arquivo de índice composto.  
  
 PARA *lExpression*  
 Especifica uma condição na qual somente os registros que satisfazem a expressão de filtro *lExpression* estão disponíveis para exibição e acesso; chaves de índice são criadas no arquivo de índice para apenas os registros que correspondem à expressão de filtro.  
  
 Tecnologia do Visual FoxPro Rushmore otimiza um índice... PARA *lExpression* comando se *lExpression* é uma expressão otimizável. Para melhor desempenho, use uma expressão otimizável na cláusula FOR.  
  
 COMPACT  
 Cria um arquivo. idx compact.  
  
 EM ORDEM CRESCENTE  
 Especifica uma ordem crescente para o arquivo. cdx. Por padrão,. cdx marcas são criadas em ordem crescente. (Você pode incluir CRESCENTE como um lembrete de pedido do arquivo de índice). Uma tabela pode ser indexada em ordem inversa, incluindo DECRESCENTE.  
  
 EM ORDEM DECRESCENTE  
 Especifica uma ordem decrescente para o arquivo. cdx. Você não pode incluir DECRESCENTE ao criar os arquivos de índice. idx.  
  
 UNIQUE  
 Especifica que apenas o primeiro registro encontrado com um valor de chave de índice específico está incluído em um arquivo. idx ou marca. cdx. UNIQUE pode ser usado para impedir o acesso ou a exibição de registros duplicados. Todos os registros adicionados com chaves de índice duplicadas são excluídos do arquivo de índice. Usando a opção exclusiva do índice é idêntico ao UNIQUE definida como ON em execução antes de emitir o índice ou a REINDEXAÇÃO.  
  
 Quando um índice exclusivo ou uma marca de índice está ativa e um registro duplicado é alterado de forma que as alterações de sua chave de índice, o índice ou a marca de índice é atualizada. No entanto, o próximo registro duplicado com a chave de índice original não pode ser acessado ou exibido até que você reindexar o arquivo usando a REINDEXAÇÃO.  
  
 CANDIDATO  
 Cria uma marca de índice estrutural do candidato. A palavra-chave de CANDIDATO pode ser incluída somente durante a criação de uma marca de índice estrutural; Caso contrário, o Visual FoxPro gera uma mensagem de erro.  
  
 Uma marca de índice candidato impede que os valores duplicados no campo ou combinação de campos especificados na expressão do índice *eExpression*. O termo *candidato* refere-se para o tipo de índice; porque os índices de candidato evitar valores duplicados, eles se qualifica como um candidato"" para ser um índice primário.  
  
 Do Visual FoxPro gerará um erro se você criar uma marca de índice de candidato para um campo ou uma combinação de campos que já contém valores duplicados.  
  
 ADITIVO  
 Mantém abre os arquivos de índice abertos anteriormente. Se você omitir a cláusula ADITIVO quando você cria um arquivo de índice ou de arquivos para uma tabela com índice, os arquivos de índice aberto anteriormente (exceto o índice composto estrutural) são fechados.  
  
## <a name="remarks"></a>Remarks  
 Registros em uma tabela que tem um arquivo de índice são exibidos e acessados na ordem especificada pela expressão do índice. A ordem física dos registros na tabela não é alterada por um arquivo de índice.  
  
## <a name="index-types"></a>Tipos de índice  
 Do Visual FoxPro lhe permite criar dois tipos de arquivos de índice:  
  
-   Composta. cdx arquivos de índice que contém várias entradas de índice, denominadas marcas  
  
-   arquivos de índice. idx que contém uma entrada de índice  
  
 Você também pode criar um arquivo de índice composto estrutural, que é aberto automaticamente com a tabela.  
  
> [!NOTE]  
>  Como arquivos de índice composto estrutural são abertos automaticamente quando a tabela é aberta, eles são o tipo de índice preferencial.  
  
 Inclua COMPACT para criar. idx compacta os arquivos de índice. Arquivos de índice composto são sempre compactos.  
  
## <a name="index-order-and-updating"></a>Ordem de índice e atualizando  
 Somente um índice (arquivo de índice mestre) ou uma marca (marca mestre) controla a ordem na qual a tabela é exibida ou acessada. Alguns comandos (por exemplo, busca) usam o arquivo de índice mestre ou a marca para procurar por registros. No entanto, todos os abertos. idx e arquivos de índice. cdx são atualizados como as alterações são feitas à tabela.  
  
## <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 Embora uma expressão de índice pode conter uma função definida pelo usuário, você não deve usar as funções definidas pelo usuário em uma expressão de índice. Funções definidas pelo usuário em uma expressão de índice aumentam o tempo que leva para criar ou atualizar o índice. Além disso, as atualizações de índice não podem ocorrer quando uma função definida pelo usuário é usada para uma expressão de índice.  
  
 Se você usar uma função definida pelo usuário em uma expressão de índice, do Visual FoxPro deve ser capaz de localizar a função definida pelo usuário. Quando o Visual FoxPro cria um índice, a expressão de índice é salvo no arquivo de índice, mas apenas uma referência para a função definida pelo usuário está incluída na expressão do índice.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [EXCLUIR o comando marca](../../odbc/microsoft/delete-tag-command.md)   
 [Comando do conjunto COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [Comando SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
