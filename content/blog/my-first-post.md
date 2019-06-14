---
title: My Second Post :)
date: 2019-06-13T01:01:43.000+00:00

---
Hellow Second!

{{< highlight go >}}
print('Hello world!');
{{< / highlight >}}


{{< highlight html >}}
<section id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{< /highlight >}}