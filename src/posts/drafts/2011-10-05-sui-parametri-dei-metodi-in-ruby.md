---
title: Sui parametri dei metodi in Ruby
author: Giustino Borzacchiello
type: post
date: 2011-10-05T21:30:46+00:00
draft: true

dsq_thread_id:
  - 899949163
categories:
  - Thoughts

  - Array
  - Metodi
  - Parametri
  - Ruby

---
Un metodo (o funzione) in Ruby può accettare zero o più parametri:

<pre class="prettyprint">class Document
  attr_accessor :title, :author, :content

  def initialize(title, content, author)
    @title = title
    @author = author
    @content = content 
  end

  def words
    @content.split
  end

  def word_count
    words.size 
  end
end
</pre>

In questo esempio, `initialize` accetta tre parametri, mentre `words` e  
`word_count` accettano zero parametri. Fin qui tutto semplice ed in linea con  
gli altri linguaggi di programmazione.

È possibile rendere alcuni parametri opzionali, fornendo un valore di default: 

<pre class="prettyprint">class Document
  attr_accessor :title, :author, :content

  def initialize(title, content, author='unknown')
    @title = title
    @author = author
    @content = content 
  end

  . . . 

  def word_count
    words.size 
  end
end
</pre>

In questo esempio modificato, `initialize` può accettare sia tre parametri, come  
prima, sia soltanto i primi due, impostando il terzo parametro al valore  
predefinito. Il risultato, ad esempio:

<pre class="prettyprint">irb %> Document.new('Prima poesia della storia umana', 'Urgh! Argh!')
 => #&lt;Document:0x9855b20 @title="Prima poesia della storia umana", @author="unknown", @content="Urgh! Argh!"&gt;
</pre>

A volte è però necessario avere un elenco completamente arbitrario di parametri:  
per questa evenienza Ruby ha una sintassi particolare:

<pre class="prettyprint">class Post
  # resto della classe

  def add_tags( *tags )
  	@tags += "#{ tags.join(" "}"
  end

  def post_meta
  ...
  end
end
</pre>

Preponendo un `*` davanti al nome del parametro, Ruby passa al metodo tutti i  
valori, &#8220;impacchettandoli&#8221; in un array che è possibile ispezionare all&#8217;interno  
del metodo. Una utile prova potrebbe essere:

<pre class="prettyprint">def stampa( *params )
  params.each do |param|
    puts param
  end
end
</pre>

Inoltre l&#8217;operatore `*` (_splat_) funziona anche in senso inverso. Riprendendo l&#8217;esempio della classe `Document`, è possibile passare un array contenente i tre elementi richiesti preponendolo con un `*`: 

<pre class="prettyprint">libro = ["L'identità", "Un albergo...", "Kundera"]
Document.new( *libro )
</pre>

Per ora mi fermo qui. Integrerò la pagina con altre informazioni in proposito.