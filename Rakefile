require 'rake/clean'
require 'json'

PREFIXES = ['braille-ja-table', 'braille-ja-table-reversed']
SOURCE = PREFIXES.map{ |prefix| "#{prefix}-source.tsv" } # raw japanese => escaped braille

CLOBBER.include PREFIXES.product(%w[escaped raw].product(%w[tsv json])).map{|p,(f,s)| "#{p}-#{f}.#{s}"}

task default: %w[tsv json]
task tsv: PREFIXES.product(%w[raw escaped]).map{|p,s| "#{p}-#{s}.tsv"}
task json: PREFIXES.product(%w[raw escaped]).map{|p,s| "#{p}-#{s}.json"}

def escape(s)
  s.ascii_only? ? s : escape_multibyte(s)
end

def escape_multibyte(s)
  s.unpack('U*').map{|n| '\u' + n.to_s(16)}.join
end

def unescape(s)
  [s[2..-1].to_i(16)].pack('U*')
end

def json(h)
  JSON.pretty_generate(h, indent: '  ')
end

PREFIXES.zip(SOURCE).each do |prefix, s|
  source_table = IO.foreach(s).inject({}) do |acc, line|
    *list = line.chomp.split("\t")
    if list.size == 2
      ja, br_escaped = *list
      acc.merge!(ja => br_escaped.scan(/.{6}/).map{|s| unescape(s)}.join)
    else
      acc
    end
  end

  desc 'create raw TSV'
  file "#{prefix}-raw.tsv" => s do |target|
    tsv = source_table.map {|pair| pair.join("\t")}.join("\n")
    IO.write(target.name, tsv << "\n")
  end

  desc 'create escaped TSV'
  file "#{prefix}-escaped.tsv" => s do |target|
    tsv = source_table.map {|pair| pair.map{|s| escape(s)}.join("\t")}.join("\n")
    IO.write(target.name, tsv << "\n")
  end

  desc 'create raw JSON'
  file "#{prefix}-raw.json" => s do |target|
    IO.write(target.name, json(source_table))
  end

  desc 'create escaped JSON'
  file "#{prefix}-escaped.json" => s do |target|
    table = source_table.inject({}) do |acc, pair|
      e = pair.map{|s| escape(s)}
      acc.merge!(e[0] => e[1])
    end
    IO.write(target.name, json(table).gsub('\\' * 2, '\\'))
  end
end