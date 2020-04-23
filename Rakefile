# -*- coding: utf-8 -*-
require 'rake/clean'

def sort_by_reading(ary)
  ary.sort_by{|l|
    fs = l.chomp.split("\t")
    fs << '-' if fs.size == 3
    raise "l must have 4 columns: #{fs.to_s}" if fs.size != 4
    reading = fs[2]
    reading_normalized = reading.gsub(/[^あ-ん]/, '')
  }
end

file 'terms.tsv' => 'orig/terms.txt' do |t|
  cp t.source, t.name
end

file 'terms_sorted.tsv' => 'terms.tsv' do |t|
  lines = File.readlines(t.source, encoding: 'UTF-8')
  header, body = lines[0], lines[1..-1]
  lines_sorted = header + sort_by_ja_alpha(body).join
  File.open(t.name, 'wb', encoding: 'UTF-8'){|f| f.write(lines_sorted)}
end

CLEAN.include('terms.tsv', 'terms_sorted.tsv')

task :default => 'terms_sorted.tsv'
